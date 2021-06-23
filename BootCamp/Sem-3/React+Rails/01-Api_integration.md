# React and Rails API Integration

Normally we start with an application that has been created using dummy data before the API is created or while the API is created so what we need to do in most cases is put our API into a premade codebase.

## React & Axios

Axios is 7kb in size which is why people don't like it although that does make it slightly easier to use so in the long run is worth it. If not axios you can still use fetch.

It is important to have a new credentials.yml file each time you are programming an app as it will have the encryption key. To do so we use `EDITOR="code --wait" rails credentials:edit` This is mainly used for Knock.

So we need to add in Axios by using `yarn add axios`

A good practice would be to have a folder called config that holds api.js Inside that file we would have the following or similar

```react
import axios from 'axios';

const jokeAPI = axios.create({
    baseURL: 'http://localhost:300'	//or the url to the server
});

export default jokeAPI;
```

We then want to import this API to wherever the services for that specific API is called.

In that file to get the data from the API because we are using axious all we have to do is point it to the endpoint.

```react
import jokeAPI from '../config/api'

export const getJokes = async () => {
    const response = await jokeAPI.get('/api/jokes');
    return response.data
}
```

From this we get a response object which will let us see the jokes. 

Similarly if we want a specific joke we do so as below.

```react
export const getJoke = async (id) => {
    const response = await jokeAPI.get(`/api/jokes/${id}`)
    return response.data
}
```

and again in the random joke we would do this similarly

```react
export async function getRandomJoke(){
    const response = await jokeAPI.get('/api/jokes/random')
    return response.data
}
```

## Authorisation and Persisting a JWT

https://github.com/axios/axios

So going from we had before we need to in an authServices.js set it up to use our API. We do this as below: The data being passed into the sign up function is an object that has a username, email, password and password_confirmation.

```react
import jokeAPI from '../config/api'

export async function signUp(data){
    const response = await jokeAPI.post('/api/auth/sign_up', data);
    return response.data
}

export async function signIn(data){
    const response = await jokeAPI.post('/api/auth/sign_in', data);
    return response.data
}
```

Our log in we need to save the jwt (arguably bad practice?). We can do this similarly for a new user and not just the log in state.

```react
function handleSubmit(event){
    event.preventDefault();
    signIn(formState)
    .then(({username,jwt}) => {
        sessionStorage.setItem("token", jwt); // this holds the token
        dispatch({type: 'setLoggedInUser', data: username})
        dispatch({type: 'setToken', data: jwt})
        history.push('/')
    })
    .catch((error) => console.log(error))
}
```

After we do this we have the ability to access all of this in our axios instance in the jokeAPI. We do this as follows

```react
import axios from 'axios';

const jokeAPI = axios.create({
    baseURL: "http://localhost:3000"
})

jokeAPI.interceptors.request.use((req) => {
    const token = sessionStorage.getItem('token')
    if (token) {
        req.headers["Authorization"] = `Bearer ${token}`
    }
    return req
})

export default jokeAPI;
```

After we  handle this we need to now maintain the logged in use and we do this in the sign in section

```react
function handleSubmit(event){
    event.preventDefault();
    signIn(formState)
    .then(({username,jwt}) => {
        sessionStorage.setItem("token", jwt);
        sessionStorage.setItem("user", username); // new line
        dispatch({type: 'setLoggedInUser', data: username})
        dispatch({type: 'setToken', data: jwt})
        history.push('/')
    })
    .catch((error) => console.log(error))
}
```

We then can handle this in the initial state as seen in the main app

```react
const App = () => {
    const initialState = {
        jokes: [],
        loggedInUser: sessionStorage.getItem("user") || null,
        auth: {token: sessionStorage.getItem("token") || null}
    }
}
```

Finally we need to create a sign out function which we do in auth services

```react
export async function signOut(data) {
    sessionStorage.clear();
    return "Logged out";
}
```

And again in the handle sign out

```react
function handleSignOut(event) {
    event.preventDefault()
    signOut(loggedInUser)
    .then(() => {
        dispatch({type: 'setLoggedInUser', data:null})
        dispatch({type: 'setToken', data:null})
    })
}
```

## Use token to create/delete jokes

```react
export async function createJoke(joke){
    const response = await jokeAPI.post('/api/jokes', joke)
    return response.data
}

export async function deleteJoke(id){
    const response = await jokeAPI.delete(`/api/jokes/${id}`)
    return response.data
}

export async function updateJoke(data){
    const respose = await jokeAPI.put(`/api/jokes/${id}`, {body: data.body, categorey_id: data.category_id})
    return response.data
}
```

