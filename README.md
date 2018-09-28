## Objective
Main objective of this blog post is to give you an idea about how to use Music Visualization in Unity.

The image below will give you a better idea on what will be the outcome at the end. 

![](http://www.theappguruz.com/app/uploads/2015/06/music-edit-300x188.png)

## Step 1 : Create Project

Create a new project named “Music Visualization” in Unity 2D.

## Step 2 : White Color Strip

Take a small strip with white color.
You can download it from here.

![](http://www.theappguruz.com/app/uploads/2015/06/bar-300x136.png)


## Step 3 : Make Prefab

Make the prefab of the strip.

## Step 4 : Apply Prefab

Now, drag that prefab into the scene, we need 64 objects of that prefab.
Now, set all the objects parallel to each other as shown below.

**Note :**
- You can use a number of objects according to your own logic.
- In this example, I have used 44 objects with an array of size = 64(44 is less than 64).

![](http://www.theappguruz.com/app/uploads/2015/06/sound-edit-300x268.png)

## Step 5 Create Script

Create a new C# script and give it a name, BarVisulization.cs.

**BarVisulization.cs:**
```csharp
Using UnityEngine;
using System.Collections;
using UnityEngine.UI;
 
[RequireComponent(typeof(AudioSource))]
public class BarVisulization : MonoBehaviour
{
        public AudioClip[] clips;
        public SpriteRenderer[] barsSprites;
        public Slider musicSlider;
        [Range(0,10)]
        public float
                colorMultiplyer = 1;
        [Range(0,1)]    
        public float
                s = 1;
        [Range(0,1)]
        public float
                v = 1;
        private int index = 0;
        private float musicLength;
    
        void Update ()
        {
                Visulization ();
                if (Input.GetMouseButtonDown (0)) {
                        ChangeSound ();
                }
        MusicSlider();
        }
 
        void Visulization ()
        {
                float[] musicData = audio.GetSpectrumData (64, 0, FFTWindow.Triangle);
                int i = 0;
                while (i clips.Length - 1) {
                        index = 0;
                }
                print (index);
                audio.clip = clips [index];    
                
                audio.Play ();
        }
 
 
    #region Static
        public static Color HSVtoRGB (float hue, float saturation, float value, float alpha)
        {
                while (hue > 1f) {
                        hue -= 1f;
                }
                while (hue  1f) {
                        saturation -= 1f;
                }
                while (saturation  1f) {
                        value -= 1f;
                }
                while (value  0.999f) {
                        hue = 0.999f;
                }
                if (hue  0.999f) {
                        saturation = 0.999f;
                }
                if (saturation  0.999f) {
                        value = 0.999f;
                }
                if (value < 0.001f) {
                        value = 0.001f;
                }
        
                float h6 = hue * 6f;
                if (h6 == 6f) {
                        h6 = 0f;
                }
                int ihue = (int)(h6);
                float p = value * (1f - saturation);
                float q = value * (1f - (saturation * (h6 - (float)ihue)));
                float t = value * (1f - (saturation * (1f - (h6 - (float)ihue))));
                switch (ihue) {
                case 0:
                        return new Color (value, t, p, alpha);
                case 1:
                        return new Color (q, value, p, alpha);
                case 2:
                        return new Color (p, value, t, alpha);
                case 3:
                        return new Color (p, q, value, alpha);
                case 4:
                        return new Color (t, p, value, alpha);
                default:
                        return new Color (value, p, q, alpha);
                }
        }
    #endregion
}
```

**Notes:**

```csharp
float [ ] musicData = audio.GetSpectrumData (64, 0, FFTWindow.Triangle);
```

This function gives a float array with Spectrum value of the audio clip. For more information, click here.

Here, I have used HSVtoRGB() function that converts HSVcolor to RGB color.
HSV colors are easy to understand. To know more about HSV colors, [click here](http://docs.unity3d.com/ScriptReference/AudioSource.GetSpectrumData.html)

![](http://www.theappguruz.com/app/uploads/2015/06/untitled-300x154.png)

## Step 6 : Apply Script

Drag the script to an empty object.

Select all 44 Bar Gameobjects and drag them on barSprites (reference to the public array barSprites, declared in BarVisulization.cs file).

![](http://www.theappguruz.com/app/uploads/2015/06/main-camera-left-right-300x194.png)

## Step 7 : Set Camera

Set Camera background color to some dark color. 

![](http://www.theappguruz.com/app/uploads/2015/06/game-300x202.png)

## Step 8 : Audio Clip

You will also need some audio clips for demonstration.

Import your audio files into your project and drag all of them on to the clips. (reference to the public array clips, declared in BarVisulization.cs file). 

![](http://www.theappguruz.com/app/uploads/2015/06/bar-visulaization-300x142.png)

## Step 9 : Test

Now, you are ready to go. Press the play button and enjoy your music with lots of different colors on your bar sprites.
