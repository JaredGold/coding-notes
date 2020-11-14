# Rocket Code

Below is the code used in the rocket ship code. I will break it up so that way it makes more sense and is easier to read. This needs to be tweaked as a lot of it should not be on the one object. At least this gives an idea of what needed to be done.

```C#
using UnityEngine;
using UnityEngine.SceneManagement;

public class Rocket : MonoBehaviour {
    [SerializeField] float rcsThrust = 100f; //Sideways Thrust power
    [SerializeField] float mainThrust = 100f; //Upward Thrust power
    [SerializeField] float levelLoadDelay = 2f;
    [Header("Audio References")]
    [SerializeField] AudioClip mainEngine;
    [SerializeField] AudioClip success;
    [SerializeField] AudioClip death;
    [Header("Particle References")]
    [SerializeField] ParticleSystem mainEngineParticles;
    [SerializeField] ParticleSystem successParticles;
    [SerializeField] ParticleSystem deathParticles;

    bool isTransitioning = false;
    bool collisionsEnabled = true;
    Rigidbody rigidBody;
    AudioSource audioSource;

	void Start ()
    {
        rigidBody = GetComponent<Rigidbody>(); //create an easily accesable component tag
        audioSource = GetComponent<AudioSource>(); // as above

	}
	
	void Update ()
    {
        if (!isTransitioning)
        {
            RespondToThrustInput();
            RespondToRotateInput();

            if (Debug.isDebugBuild) // only called if in Debug
            {
                RespondToDebugKeys();
            }
        }
    }

    private void RespondToDebugKeys() 
    {
        if (Input.GetKeyDown(KeyCode.L))
        {
            LoadNextLevel();
        }
        if (Input.GetKeyDown(KeyCode.C))
        {
            if (collisionsEnabled) { collisionsEnabled = false; }
            else if (!collisionsEnabled) { collisionsEnabled = true; }
        }
    }

    void OnCollisionEnter(Collision collision)
    {
        if (isTransitioning || !collisionsEnabled) { return; } // ignore collisions
       
        switch (collision.gameObject.tag)
        {
                case "Friendly":
                    // do nothing
                    break;
                case "Finish":
                    StartSuccessSequence();
                    break;
                default:
                    StartDeathSequence();
                    break;
        }
    }

    private void StartSuccessSequence()
    {
        isTransitioning = true;
        audioSource.Stop();
        audioSource.PlayOneShot(success);
        successParticles.Play();
        Invoke("LoadNextLevel", levelLoadDelay);
    }

    private void StartDeathSequence()
    {
        isTransitioning = true;
        audioSource.Stop();
        audioSource.PlayOneShot(death);
        mainEngineParticles.Stop();
        deathParticles.Play();
        Invoke("ReloadCurrentLevel", levelLoadDelay);
    }

    private void LoadNextLevel()
    {
        int currentSceneIndex = SceneManager.GetActiveScene().buildIndex; // create a count of what current scene we are on
        int nextSceneIndex = currentSceneIndex +1; // add one to current scene index
        if (nextSceneIndex == SceneManager.sceneCountInBuildSettings)
        {
            nextSceneIndex = 0; //  loop back to start
        }
        SceneManager.LoadScene(nextSceneIndex);
    }

    private void ReloadCurrentLevel()
    {
        int currentSceneIndex = SceneManager.GetActiveScene().buildIndex; // create a count of what current scene we are on
        SceneManager.LoadScene(currentSceneIndex);
    }

    private void LoadFirstLevel()
    {
        SceneManager.LoadScene(0);
    }

    private void RespondToThrustInput()
    {
        if (Input.GetKey(KeyCode.Space) || Input.GetKey(KeyCode.W)) // can thrust while rotating
        {
            ApplyThrust();
        }
        else
        {
            StopApplyingThrust();
        }
    }

    private void StopApplyingThrust()
    {
        audioSource.Stop();
        mainEngineParticles.Stop();
    }

    private void ApplyThrust()
    {
        rigidBody.AddRelativeForce(Vector3.up * mainThrust * Time.deltaTime);
        if (!audioSource.isPlaying) // so it doesn't layer
        {
            audioSource.PlayOneShot(mainEngine);
            mainEngineParticles.Play();
        }
    }

    private void RespondToRotateInput()
    {
        rigidBody.angularVelocity = Vector3.zero; // remove rotation due to physics
       
        float rotationThisFrame = rcsThrust * Time.deltaTime;
        if (Input.GetKey(KeyCode.A))
        {
            transform.Rotate(Vector3.forward * rotationThisFrame);
        }
        else if (Input.GetKey(KeyCode.D))
        {
            transform.Rotate(-Vector3.forward * rotationThisFrame);
        }
    }
}
```

# Oscillator Code

``` C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[DisallowMultipleComponent] // only allows this script to be put on an object once (no dulplicates of itself)
public class Oscillator : MonoBehaviour
{
    [SerializeField] Vector3 movementVector = new Vector3(10f, 10f, 10f);
    [SerializeField] float speed = 2f;

    // todo remove from inspector later
    float movementFactor; // 0 for not moved, 1 for fully moved
    Vector3 startingPos;

    void Start()
    {
        startingPos = transform.position;   
    }

    void Update()
    {
        if (speed <= Mathf.Epsilon) { return; } // protect from speed being Null (NaN fix) 
                                                //Mathf.Epsilon is the smallest possible number (lowest possible number without NaN)
        float cycles = Time.time / speed;       // grows continually from 0

        const float tau = Mathf.PI * 2;         // about 6.28
        float rawSinWave = Mathf.Sin(cycles * tau); // cycles from -1 to +1 (SMOOTHLY)

        movementFactor = rawSinWave / 2f + 0.5f ;
        Vector3 offset = movementFactor * movementVector;
        transform.position = startingPos + offset;
    }
}

```

