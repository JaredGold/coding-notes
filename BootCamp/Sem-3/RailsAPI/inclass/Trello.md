# Step by step commands to create rails app

1. Create the api : `rails new super-awesome-api --api --database=postgresql`

2. CD into the api `cd super-awesome-api`

3. Create the scaff : `rails g scaffold item:text` (you can add more... look into docs)

4. Go back to the main folder `cd ..`

5. Create the app `npx create-react-app super-awesome-client`

6. CD into the react app `cd super-awesome-client`

7. install axios `yarn add axios`

8. Test everything with use effect

   ```react
   import {useEffect} from "react"
   import axios from 'axios'
   
   function App() {
     useEffect(() => {
       axios.get("http://localhost:4000/cards")
         .then(res => console.log(res))
     }, []);
   ```

9. In the server add cors in the bundle file (uncomment)

10. Then in initializers uncomment the core code

11. Then run a `bundle install`

12. Start the server using `rails s -p 4000`

13. In the react app add `"start:local": "REACT_APP_API_URL=http://localhost:4000 react-scripts start",` to the package.json

14. Now change in the app 

    ```react
    const apiUrl = process.env.REACT_APP_API_URL
    
    function App() {
      useEffect(() => {
        axios.get(`${apiUrl}/cards`)
    ```

15. Restart the server but run `yarn start:local`

OPTIONAL - Install material ui following https://material-ui.com/

Updated react app

```react
import {useEffect, useState} from "react"
import axios from 'axios'
import {Button, Typography, Box} from '@material-ui/core'
import './App.css';

const apiUrl = process.env.REACT_APP_API_URL

function App() {
  const [cards, setCards] = useState([])

  useEffect(() => {
    axios.get(`${apiUrl}/cards`)
      .then(({data}) => setCards(data))
  }, []);


  return (
    <div className="App">
      <Typography>
        Trello Clone
      </Typography>
      <Button variant="outlined">This is a button</Button>
      {cards.map(({title, description, id}) => (
        <Box key={id}>
          <Typography>Title: {title}</Typography>
          <Typography>Description: {description}</Typography>
        </Box>
      ))}
    </div>
  );
}

export default App;

```

---

# Day 2

On day 2 we posted the API to heroku and had to change cors to allow for where our front end is going to be deployed.

We also added a Procfile ot the root of the api and added the below. This tells Heroku specifically what to do on release. The below could possibly need to be a rake.

```
release: rails db:migrate
```

We then jumped into netlify and deployed our front end. 

We then updated our Cors to allow our netlify link and did a push.

We then need to update the correct apiUrl by updating the data index.js

```js
let apiUrl;

if (process.env.NODE_ENV === "production"){
  apiUrl = "https://blabla.herokuapp.com" // wherever the api is hosted
} else {
  apiUrl = process.env.REACT_APP_API_URL
}
```

After that just more customisations
