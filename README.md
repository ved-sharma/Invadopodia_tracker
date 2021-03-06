# Invadopodia tracker  
<img src="Invadopodia tracking movie_v2.gif" alt="Invadopodia tracking movie_v2">  

**Movie:** Invadopodia tracking in a time-lapse movie of a carcinoma cell. Tracked invadopodia are shown in red circles. Time is in min:sec and movie is played at 20 fps.


This page gives detailed description of how to use "Invadopodia tracker" plugin to analyze invadopodia dynamics (e.g. first frame of invadopodia appearance, last frame of invadopodia disappearance, invadopodia lifetime and x-y coordinates of invadopodia in each frame) from time-lapse fluorescence movies. Plugin was published in a methods chapter<sup>1</sup> and has been successfully used to track invadopodia in MTLn3, mammary carcinoma cells<sup>2</sup> and MDA-MB-231, human breast cancer cells<sup>3,4,5</sup>.

**References**

1. Sharma VP, Entenberg D, Condeelis J. High-resolution live-cell imaging and time-lapse microscopy of invadopodium dynamics and tracking analysis. Methods Mol Biol, 2013; 1046:343-57
2. Sharma, VP, Eddy R, Entenberg D, Kai M, Gertler F, Condeelis J. Tks5 and SHIP2 regulate invadopodium maturation, but not initiation, in breast carcinoma cells. Curr Biol, 2013 Nov 4; 23(21):2079-89
3. Beaty BT, Sharma VP, Bravo-Cordero JJ, Simpson MA, Eddy RJ, Koleske AJ, Condeelis J. β1 integrin regulates Arg to promote invadopodial maturation and matrix degradation. Mol Biol Cell, 2013 Jun; 24(11):1661-75
4. Beaty BT, Wang Y, Bravo-Cordero JJ, Sharma VP, Miskolci V, Hodgson L, Condeelis J. Talin regulates moesin-NHE-1 recruitment to invadopodia and promotes mammary tumor metastasis. J Cell Biol. 2014 Jun 9;205(5):737-51
5. Valenzuela-Iglesias A, Sharma VP, Beaty BT, Ding Z, Gutierrez-Millan LE, Roy P, Condeelis JS, Bravo-Cordero JJ. Profilin1 regulates invadopodium maturation in human breast cancer cells. Eur J Cell Biol. 2015 Feb;94(2):78-89
6. Cmoch A, Groves P, Pikuła S. Biogenesis of invadopodia and their cellular functions. Postepy Biochem. 2014;60(1):62-8. PMID: 25033543
7. Collins KB, Kang H, Matsche J, Klomp JE, Rehman J, Malik AB, Karginov AV. Septin2 mediates podosome maturation and endothelial cell invasion associated with angiogenesis. J Cell Biol. 2020 Feb 3;219(2):e201903023. PMID: 31865373
8. Burton KM, Cao H, Chen J, Qiang L, Krueger EW, Johnson KM, Bamlet WR, Zhang L, McNiven MA, Razidlo GL. Dynamin 2 interacts with α-actinin 4 to drive tumor cell invasion. Mol Biol Cell. 2020 Mar 15;31(6):439-451. PMID: 31967944

## Installation  
Put <a href="Invadopodia_tracker_v03.class" download>Invadopodia_tracker_v03.class<a/> file in the plugins folder and restart ImageJ. "Invadopodia tracker v03" command should now be visible under Plugins menu.

## Source code  
<a href="Invadopodia_tracker_v03.java" download>Invadopodia_tracker_v03.java<a/>

## Description
Following is a flow diagram (taken from ref 1) of how Invadopodia tracker plugin works. The description of individual steps "a" through "h" can be found in ref 1.

![image1](image1.png)

Briefly, "Invadopodia tracker" plugin works on an 8-bit or preferably 16-bit single channel fluorescence time-lapse stack. Open the stack. Choose the invadopodia you want to track by clicking on it with a "Point" tool (See Error #1 in Error messages section). Multiple-point tool can be used for selecting more than one invadopodia. Run "Invadopodia tracker v03" plugin. A dialog window (shown below) pops up, where user needs to enter a few parameters (described in detail later on). After a successful run, tracker marks each invadopodium with a red circle and writes the invadopodium trajectory coordinates in a log window. The values are tab-delimited, so these can be directly copied and pasted into an Excel file for further processing (e.g. to calculate invadopodia lifetime, velocity, total distance and net distance traveled). The first column is the frame number; second and third columns are the x and y coordinates, respectively.

![image2](image2.png)

<ins>Max invadopod displacement (pixels)</ins>

... is the maximum displacement of the invadopod, in pixels, from one frame to the next.

<ins>Estimate of min/max no. of invadopods:</ins>

To identify invadopodia, user needs to provide an estimate of the average number of min and max invadopodia per frame in the time-lapse movie. This can be easily estimated by using Process > Find Maxima... command with preview ON and playing around with different noise tolerance values.

**Note 1:** After running the Invadopodia tracker plugin, if user finds that the plugin is not tracking the invadopodia throughout i.e. plugin misses some frames during the appearance and/or disappearance of the invadopodia, then user should increase the estimates of min and max no. of invadopodia.

**Note 2:** As the estimates for min and max no. of invadopodia goes up, tracker might find too many invadopodia and might get confused in linking the invadopodium correctly form one frame to the next frame. On the other hand, as the estimates for min and max no. of invadopodia go down, tracker might miss the not-so-bright invadopodia, which is usually the case during the appearance and disappearance of the invadopodium.

Noise tolerance, Delta noise tolerance and Max iterations are the next three parameters, which are set by default and change automatically when the user runs the plugin. These parameters were incorporated into the main user-interface of the plugin for advanced user to identify the problem in case the plugin is not tracking invadopodia properly.

The information about length unit (e.g. pixels or microns) and the time it takes for the plugin to track the invadopodia appears in the log window and can be suppressed by checking the appropriate box. The information about invadopodia X-Y coordinates in each frame can be also be suppressed by checking the appropriate box. This comes in handy when user is only interested in invadopodia lifetimes.

## Handling error messages
**Error #1**  
![image3](image3.png)

This one is pretty obvious that the plugin did not find any invadopod(s) within 5 pixels (user defined "Max invadopod displacement" parameter) of point ROI. Draw the point ROI closer to the actual invadopod maxima.

**Error #2**  
![image4](image4.png)

Here, user defined  the estimates of min and max no. of invadopodia as 150 and 200, respectively. Plugin found 146 invadpodia at noise tolerance (NT) value of 14 (previous iteration) and by lowering NT to 13, plugin finds 211 invadopodia (current iteration). Meaning, to converge to a solution, the invadopodia min - max range needs to be increased by either decreasing the estimate of min no. of invadopodia (to less than or equal to 146; a good guess is 125) and/or increasing the estimate of max no. of invadopodia (to more than or equal to 211; a good guess is 225).

## Running "Invadopodia tracker" plugin from a macro
The plugin is macro recordable, which makes it possible to analyze a lot of invadopodia in a high-throughput fashion. Select each invadopodium with a point ROI and add them to ROI Manager (note: all ROIs need not be on a single frame) and then run the following macro (default parameters are shown; user needs to adjust these based on his/her data):

```
// macro starts here
n = roiManager("count");
for(i=0;i<n;i++) {
roiManager("Select", i);
run("Invadopodia tracker v03", "max=5 estimate=200 estimate_=300 noise=500 delta=20 max_=200 suppress suppress_");
}
// macro ends here
```

<sub>Published: November 20, 2013</sub>  
<sub>Last update: February 16, 2015</sub>
