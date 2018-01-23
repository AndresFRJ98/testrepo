# Fizzyo Project User Guide
A Unity package for Fizzyo game development


## Installation
Download the latest Fizzyo Framework unity package from [here](https://github.com/Fizzyo)

- From Unity **select Assets** > **Import Package** > **Custom Package**
- Select the **FizzyoFramework.unitypackage** that you have downloaded.
- In the window that pops up select **ok** to import the package.
- Alternatively you can move the folder called Fizzyo inside the downloaded to the assests in your unity game directory. 

*the Unity package is also able to be cloned directly from GitHub and the fizzyo folder placed in your projects Assets folder.*

## About the framework
After importing the framework, you will have a folder called Fizzyo in your Assets directory. The folder contains everything you will need to make a Fizzyo game. The Fizzyo framework consists of singleton methods which you call when you need them.
You will not need to modify anything.



## How to use
How to use these will be explained with an example space shooter game, which uses the Fizzyo device as a controller.
The basic principle of this space shooter game is:
-          The player controls the space ship to move left and right
-          The player is able to shoot lasers to destroy enemies.

And the Fizzyo device has two possible inputs, breath detection and a button. The example game will have the player breath input to shoot the lasers, and the button to control the player movement.

## Breath detection
```csharp
 void OnBreathStarted(object sender)
    {
     
    }

void OnBreathEnded(object sender, ExhalationCompleteEventArgs e)
    {

    }

```

This set of code allows the game to read breath inputs from the device. You must first initialise the first two lines, and the following code tells your game what to do at the start of a breath and the end of a breath. 

In the example game, the game is designed to shoot the laser upon a breath input. This is a part of the code for shooting lasers, a script attached on the play object.

```chsarp
void OnBreathStarted(object sender)
    {
        gameObject.transform.GetChild (0).gameObject.SetActive (true);
    }

 void OnBreathEnded(object sender, ExhalationCompleteEventArgs e)
    {
        gameObject.transform.GetChild (0).gameObject.SetActive (false);
    }
```

In this game, when there is a breath detected, the laser game object, which is a child object of the player object, is set active to true (laser appears), and at the end of a breath it is set to false (laser disappears).

### Using the button

The ButtonDown() is a boolean class, which returns true when the button is pressed and false when it is not. (You can also use Input.GetButtonDown("Fire1"))

```csharp
public bool ButtonDown()
        {
            return Input.GetButtonDown("Fire1");
        }

```

An example from the space shooter game, where the player controls the spaceship using the button on the device.

```csharp
void movePlayer(){
        if (FizzyoFramework.Instance.Device.ButtonDown() == true) {

            if (moveDir == true) {
                Vector3 position = this.transform.position;
                position.x += 0.2f;
                if (position.x < 5.5f) {
                    this.transform.position = position;
                } 

                else {
                    
                    moveDir = false;

                }

            } else if (moveDir == false) {
                Vector3 position = this.transform.position;
                position.x -= 0.2f;
                if (position.x > -5.5f) {
                    this.transform.position = position;
                }

                else {
                    
                    moveDir = true;

                }
            }

        }
    }

```

This is a class from a script attached to the player game object, which is called when the button on the device is pressed. The player moves in one direction, left or right until the player reaches the end of the screen, then moves in the other direction.




