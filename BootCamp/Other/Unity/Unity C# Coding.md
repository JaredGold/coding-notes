# Unity C# Coding

This code line tutorials were all done on the 3D (Section 3) tutorials on [Udemy](https://www.udemy.com/). I will leave a break between different statements and it should all be accessible on the sidebar [Outline] to make it easier 

> "This will be easy"
> 	*- Jared Goldstein*

## Git and Repository Control

* Git is a Version Control System(VCS)
* The project folder contains a repository (repo)
* We commit changes to the repo
* I have started using SourceTree which is also known as a GUI
* GitHub / BitBucket host repos remotely online

## If and Switch Statements

If and Switch statements are statements which run "IF" something is happening. Similarly switch runs the same way. An example of a switch statement is below (Found in Project_Boost). In a switch statement you use:

* "Case" the thing that's different
* "Break" used to stop Code *(Similar to an ending bracket)*
* "Default" similar to an 'Else' statement used in If statements.

```C#
    private void OnCollisionEnter(Collision collision) // When this happens (Could use a called method)
    {
        switch (collision.gameObject.tag) // get the tag and do whatever the tags case is
        {
            case "Friendly": // if the tag is friendly
                print("OK"); // do this
                break; // then stop
            case "Fuel": // if it is this
                print("You've touched fuel"); // do this
                break; // then stop
            default: // if it is anything else
                print("You have been killed by" + collision.collider); // do this
                break; // then stop
        }
    }
```

## States - Enum

States can be used to change the current state of the player or similar in code. For example below is states used in Project_Boost to switch between being alive or dead or similar.

```C#
    enum State { Alive, Dying, Transcending} // create the term State and it's children
    State state = State.Alive; // Create the term state and set value by default
```

## Invoke

Invoke can be used to do something after said amount of time. Unfortunately this has to be called in string form (not the best to use string forms). This may not be as good as IEnumerators.

```C#
            case "Finish":
                Invoke("LoadNextScene", 1f); // todo parameterise time
                break;

    private void LoadNextScene()
    {
        SceneManager.LoadScene(1);
    }
```

