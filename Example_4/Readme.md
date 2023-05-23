 Example_4

## Description
Name: ERTMS_Test_Plant.RailAID

This example is mentioned in the manuscript titled: "Automatic Railway Signalling Generation for Railways Systems Described on Railway Markup Language (railML)". Henceforth, when we refer to the manuscript, we will do it as [[1]](#references).

## Analysis principles

The signalling generation process used in this work was designed following signalling principles detailed in [[1]](#references) in the section "I. INTRODUCTION".

## Step by step

The following is the general methodology or "step by step" followed for analysing a railway network with the approach of this work [[1]](#references).

A. Import the railway layout description.

B. Define a graph network to associate the railway elements.

C. Infrastructure analysis

D. Detect CDL zones.

E. Generate signalling.

F. Simplify signalling.

G. Export a resulting railway layout description.

Each step is explained below.

### A. Import the railway layout description

After having installed the RNA program according to the steps shown in the the section ["Usage"](https://github.com/GICSAFePhD/Layouts#usage), run the Python archive "main_GUI.py". This action produces the program output shown in Figure 1.

![Figure 1](select_example.jpg "Figure 1")

*Figure 1. Select example.*

The necessary information to define the graph network is distributed across several sections of the railML file, specifically inside netElements (nodes) and netRelations (edges) items found in the class Infrastructure/Topology as described in [[1]](#references).

Figure 2 shows the railway network without signalling. The user will need the Design4Rail Horizon Software Suite Track Planner application and import the archive "Example_2.railml" to visualise the railway network used in this example. 

For further information about the Design4Rail Horizon Software Suite and the Track Planner application, please refer to [Official web page of Design4Rail](https://design4rail.com/service/d4rhorizon/#section-downloadHorizon).

For a detailed explanation about importing railML files, go to section [G.1](#g1-obtaining-the-interlocking-table-in-design4rail) of this document. 

![Figure 2](Figure0.jpg "Figure 2")

*Figure 2. Railway network without signalling.*

### B. Define a graph network to associate the railway elements

This step allows us to evaluate the consistency of the network connections provided in the RailML file, through the determination of the direction, position, and interconnection of each of the nodes of the given railway network.

In [[1]](#references), in the section "II. RAILWAY NETWORK ANALYZER DESIGN" in literal B, we see Algorithm 1, which explains the network analysis process.

The result of this RNA step is show in Console Output 1:

~~~
#################### Starting Railway Network Analyzer ####################
Reading .railML file
Creating railML object
Analyzing railML object
 Analyzing graph
ne991 [-1064, 0] [-2322, 0] <<
ne61 [4350, 0] [4804, 250] >> 
ne63 [4350, 0] [5763, 0] >>
ne65 [7444, 0] [5763, 0] <<
ne910 [11254, 0] [11822, 250] >>
ne912 [11254, 0] [13111, 0] >>
ne114 [15670, 0] [14482, 0] <<
ne288 [-1064, 0] [-741, 250] >>
ne290 [-1064, 0] [-211, 0] >>
ne292 [864, 0] [-211, 0] <<
ne295 [-741, 250] [457, 250] >>
ne297 [457, 250] [720, 250] >>
ne377 [350, -200] [-92, -200] <<
ne384 [457, 250] [-104, 450] <<
ne400 [6904, 250] [7194, 250] >>
ne404 [4804, 250] [6904, 250] >>
ne407 [6904, 250] [5855, 500] <<
ne421 [6454, -259] [5915, -259] <<
ne450 [14722, 250] [14232, 250] <<
ne465 [13772, -259] [13263, -259] <<
ne98 [1573, 0] [3687, 0] >>
ne99 [3687, 0] [4350, 0] >>
ne100 [8372, 0] [10727, 0] >>
ne101 [10727, 0] [11254, 0] >>
ne102 [15670, 0] [18172, 0] >>
ne104 [-509, 630] [-104, 450] >>
ne110 [-104, 450] [-741, 250] <<
ne111 [-211, 0] [-92, -200] >>
ne113 [-92, -200] [-749, -200] <<
ne122 [5304, 759] [5855, 500] >>
ne123 [5855, 500] [4804, 250] <<
ne124 [5763, 0] [5915, -259] >>
ne126 [5915, -259] [5354, -259] <<
ne127 [14232, 250] [13022, 500] <<
ne129 [14232, 250] [14482, 0] >>
ne130 [14232, 250] [11822, 250] <<
ne131 [13111, 0] [13263, -259] >>
ne132 [13111, 0] [14482, 0] >>
ne133 [13263, -259] [12722, -259] <<
ne134 [12452, 810] [13022, 500] >>
ne135 [13022, 500] [11822, 250] <<
ne992 [7444, 0] [8372, 0] >>
ne993 [7194, 250] [7504, 250] >>
ne994 [7444, 0] [7194, 250] <<
ne995 [720, 250] [1020, 250] >>
ne996 [864, 0] [1573, 0] >>
ne997 [720, 250] [864, 0] >>
 The network is connected
~~~

*Console Output 1. Step B railway elements.*

In this example, the Console Output 1 shows that the program can identify the nodes and their directions. Consol Output 1 has, for example, this line: ne61 [4350, 0] [4804, 250] >>, that indicates the name of the netElement (ne16), the position (origin [4350, 0] and end point [4804, 250]) of the net element, and the direction (>>, at right in this case, but in other example it could have been at left: <<). The same analysis stands for the other net elements. It can be noticed that Console Output 1 is consistent with every "netElement" shown in Figure 2.

### C and D. Infrastructure analysis and CDL zones detection

The process of analysing the infrastructure and detecting CDL zones allows identifying the position of each infrastructure element in the network: platforms, curves, level crossings, buffer stops, derailers, lines, operational points, signals, switches, tracks and detection elements (axle counters, rail joints and track circuits).

In section "II. RAILWAY NETWORK ANALYSER DESIGN" literal C of [[1]](#references), it is shown Algorithm 2, which explains the process of analysing the network; and in the same section but in literal D, it is explained the process used to detect CDL zones.

The result of this step is shown in Console Output 2 and Figure 3.

~~~
 Analyzing infrastructure --> Infrastructure.RNA
 Detecting Danger --> Safe_points.RNA
  ne991 has a Middle point @ [-2112.3333333333335, 0]
  ne991 has a Middle point @ [-1902.6666666666667, 0]
  ne991 has a Middle point @ [-1693.0, 0]
  ne991 has a Middle point @ [-1483.3333333333335, 0]
  ne991 has a Middle point @ [-1273.6666666666667, 0]
  ne61 has a Curve(2 lines) @ [[4600, 250]]
  ne63 has a Middle point @ [4551.857142857143, 0]
  ne63 has a Middle point @ [4753.714285714285, 0]
  ne63 has a Middle point @ [4955.571428571428, 0]
  ne63 has a Middle point @ [5157.428571428572, 0]
  ne63 has a Middle point @ [5359.285714285715, 0]
  ne63 has a Middle point @ [5561.142857142857, 0]
  ne65 has a Middle point @ [5973.125, 0]
  ne65 has a Middle point @ [6183.25, 0]
  ne65 has a Middle point @ [6393.375, 0]
  ne65 has a Middle point @ [6603.5, 0]
  ne65 has a Middle point @ [6813.625, 0]
  ne65 has a Middle point @ [7023.75, 0]
  ne65 has a Middle point @ [7233.875, 0]
  ne910 has a Curve(2 lines) @ [[11504, 250]]
  ne912 has a RailJoint[J24] @ [11867, 0]
  ne114 has a RailJoint[J27] @ [15294, 0]
  ne288 has a Curve(2 lines) @ [[-928, 250]]
  ne290 has a RailJoint[J07] @ [-633, 0]
  ne292 has a RailJoint[J05] @ [538, 0]
  ne295 has a Middle point @ [-501.4, 250]
  ne295 has a Middle point @ [-261.8, 250]
  ne295 has a Middle point @ [-22.200000000000045, 250]
  ne295 has a Middle point @ [217.39999999999998, 250]
  ne297 has a Middle point @ [588.5, 250]
  ne377 has a Middle point @ [129.0, -200]
  ne384 has a Curve(2 lines) @ [[350, 450]]
  ne400 has a Middle point @ [7049.0, 250]
  ne404 has a Middle point @ [5014.0, 250]
  ne404 has a Middle point @ [5224.0, 250]
  ne404 has a Middle point @ [5434.0, 250]
  ne404 has a Middle point @ [5644.0, 250]
  ne404 has a Middle point @ [5854.0, 250]
  ne404 has a Middle point @ [6064.0, 250]
  ne404 has a Middle point @ [6274.0, 250]
  ne404 has a Middle point @ [6484.0, 250]
  ne404 has a Middle point @ [6694.0, 250]
  ne407 has a Curve(2 lines) @ [[6654, 500]]
  ne421 has a Middle point @ [6184.5, -259]
  ne450 has a Middle point @ [14477.0, 250]
  ne465 has a Middle point @ [13517.5, -259]
  ne98 has a LevelCrossing[lcr495] @ [2419, 0]
  ne98 has a LevelCrossing[lcr496] @ [2419, 0]
  ne99 has a Middle point @ [3908.0, 0]
  ne99 has a Middle point @ [4129.0, 0]
  ne100 has a LevelCrossing[lcr497] @ [9346, 0]
  ne100 has a LevelCrossing[lcr498] @ [10127, 0]
  ne100 has a LevelCrossing[lcr499] @ [9347, 0]
  ne100 has a LevelCrossing[lcr500] @ [10127, 0]
  ne101 has a RailJoint[J26] @ [10914, 0]
  ne102 has a Middle point @ [15878.5, 0]
  ne102 has a Middle point @ [16087.0, 0]
  ne102 has a Middle point @ [16295.5, 0]
  ne102 has a Middle point @ [16504.0, 0]
  ne102 has a Middle point @ [16712.5, 0]
  ne102 has a Middle point @ [16921.0, 0]
  ne102 has a Middle point @ [17129.5, 0]
  ne102 has a Middle point @ [17338.0, 0]
  ne102 has a Middle point @ [17546.5, 0]
  ne102 has a Middle point @ [17755.0, 0]
  ne102 has a Middle point @ [17963.5, 0]
  ne104 has a Curve(2 lines) @ [[-209, 630]]
  ne110 has a Curve(2 lines) @ [[-633, 450]]
  ne113 has a Middle point @ [-530.0, -200]
  ne113 has a Middle point @ [-311.0, -200]
  ne122 has a Curve(2 lines) @ [[5704, 759]]
  ne123 has a Curve(2 lines) @ [[5054, 500]]
  ne126 has a Middle point @ [5634.5, -259]
  ne127 has a Curve(2 lines) @ [[13982, 500]]
  ne130 has a Middle point @ [12022.833333333334, 250]
  ne130 has a Middle point @ [12223.666666666666, 250]
  ne130 has a Middle point @ [12424.5, 250]
  ne130 has a Middle point @ [12625.333333333334, 250]
  ne130 has a Middle point @ [12826.166666666666, 250]
  ne130 has a Middle point @ [13027.0, 250]
  ne130 has a Middle point @ [13227.833333333334, 250]
  ne130 has a Middle point @ [13428.666666666666, 250]
  ne130 has a Middle point @ [13629.5, 250]
  ne130 has a Middle point @ [13830.333333333334, 250]
  ne130 has a Middle point @ [14031.166666666668, 250]
  ne132 has a RailJoint[J21] @ [14309, 0]
  ne133 has a Middle point @ [12992.5, -259]
  ne134 has a Curve(2 lines) @ [[12842, 810]]
  ne135 has a Curve(2 lines) @ [[12072, 500]]
  ne992 has a RailJoint[J19] @ [8046, 0]
  ne993 has a Middle point @ [7349.0, 250]
  ne995 has a Middle point @ [870.0, 250]
  ne996 has a RailJoint[J08] @ [1094, 0]
~~~

*Console Output 2. Infraestructure analysis and CDL zone detection.*

![Figure 3](step_C_and_D_2.png "Figure 3")

*Figure 3. Infrastructure analysis and CDL zones detection: GUI Output.*

Because of this network is very extensive, some of these identified elements are shown in Figure 4.

![Figure 4](step_C_and_D_graphic.png "Figure 4")

*Figure 4. Infrastructure analysis and CDL zones detection: Layout.*

### E. Generate signalling

To obtain an analysis for each network element in the program configurations, select the options you want, as shown in Figure 5.

![Figure 5](config_options.png "Figure 5")

*Figure 5. Configuration options of RNA.*

Below, in subsections E.1, E.2, E.3, and E.4, you will find the sequence of configurations used to analyze, step by step, the railway in this example.

#### E.1. Signals generated due to line borders(L) and buffer stops(T)

The configuration of the RNA GUI application needed for this step of the analysis is shown in Figure 6.

![Figure 6](config_1.PNG "Figure 6")

*Figure 6. Configuring RNA to obtain signals for line borders(L) and buffer stops(T).*

Signals are enumerated since 00 with a prefix letter to indicate which element generates them. BufferStops and LineBorders signals start with T and L, respectively. In Figure 7, we can visualise the signals generated by applying algorithm 3, explained in [[1]](#references) section "III. SIGNALLING GENERATION".

In red colour, automatically added signals are shown in Figure 7.

The RNA allocates signals close to the buffer stops. Some of these signals are:

-- Stop: *T03, T13, T15, T27, and others*

-- Departure: *T04, T16, T14, T28, and others*

The RNA allocates signals close to the line borders. RNA allocates departure signals which are: *L30, L33 and others* assigned close to every line border that belongs to a netElement whose track is longer than a configurable fixed length, as shown in FIGURE 8. To configure this parameter, please see section [G.3.3](#g33-fixed-length-parameter).

For more details about all signalls off this step, please see Figure 9. 

![Figure 7](Figure1_zoom.png "Figure 7")

*Figure 7. Zoom of some signals due to line borders(L) and buffer stops(T).*

![Figure 8](Figure1_zoom_2.png "Figure 8")

*Figure 8. Signals L30, L33 and others assigned close to line borders*

![Figure 9](Figure1.jpg "Figure 9")

*Figure 9. All signals due to line borders(L) and buffer stops(T).*

#### E.2. Signals generated due to line borders(L),buffer stops(T) and rail joints (J)

The signals for rail joints are named J and have a consecutive number of signals.

The configuration of the RNA GUI application needed for this step of the analysis is shown in Figure 10.

![Figure 10](config_2.PNG "Figure 10")

*Figure 10. Configuring RNA to obtain signals for line borders(L), buffer stops(T) and rail joints (J).*

The algorithm assign signalling at the beginning and the ending of each track as shown in Figure 11. Some of this signals are: *J34, J35, J37, J36, J38, J39 and others*. For more details about all signalls off this step, please see Figure 12. 

![Figure 11](Figure2_zoom.png "Figure 11")

*Figure 11. Zoom of some signals due to line borders(L), buffer stops(T) and rail joints (J).*

![Figure 12](Figure2.jpg "Figure 12")

*Figure 12. All signals due to line borders(L), buffer stops(T) and rail joints (J).*

#### E.3. Signals generated due to line borders(L),buffer stops(T),rail joints (J), platforms(P) and level crossings(X)

The signals for platforms are named P, and signals for level crossings are named X. A consecutive number of signals is assigned for each type of signalling.

The configuration of the RNA GUI application needed for this step of the analysis is shown in Figure 13.

![Figure 13](config_3.PNG "Figure 13")

*Figure 13. Configuring RNA to obtain signals for line borders(L),buffer stops(T),rail joints (J), platforms(P) and level crossings(X).*

Notice that RNA can be configured to avoid adding duplicate signals when the level crossing and the platform are close together, as discussed in [[1]](#references), and therefore, the signalling between them is unnecessary. However, this configuration is a special parameter in RNA. For furthermore information about this, see section [G.3.2.](#g32-minimum-distance-parameter) 

It is necessary to introduce signals before the train reaches the level crossing as explained in Algorithm 5, explained in [[1]](#references) section "III. SIGNALLING GENERATION".

Also, it is necessary to have a departure signal after the platform. This logic is implemented using Algorithm 6, explained in [[1]](#references) section "III. SIGNALLING GENERATION".

In red colour, some signals generated due level crossings and platforms are shown in Figure 14. Because of this network not have platforms, these signals are not allocated. All signals allocated, due to level crossings, for the entire are network are shown in Figure 15.

![Figure 14](Figure3_zoom.png "Figure 14")

*Figure 14. Some signals due to line borders(L),buffer stops(T),rail joints (J), platforms(P) and level crossings(X).*

![Figure 15](Figure3.jpg "Figure 15")

*Figure 15. All signals due to line borders(L),buffer stops(T),rail joints (J), platforms(P) and level crossings(X).*

#### E.4. Signals generated due to line borders(L),buffer stops(T),rail joints (J), platforms(P),level crossings(X) and switches(S,H,C,B)

The configuration of the RNA GUI application needed for this step of the analysis is shown in Figure 16.

![Figure 16](config_4.PNG "Figure 16")

*Figure 16. Configuring RNA to obtain signals for line borders(L),buffer stops(T),rail joints (J), platforms(P),level crossings(X) and switches(S,H,C,B).*

The signals for switches are named based on the point they want to protect: S for Starting branch, C for the Continue branch and B for the Detour branch. There are also signals whose name starts with H that are not explicitly protecting the starting branch, the continue branch or the detour branch of a switch. These H signals are explained in [[1]](#references) section "III. SIGNALLING GENERATION" in literal E, where a manoeuvre signal numbered with H is always added plus the corresponding numbering sequence by Algorithm 7. This manoeuvre signal always accompanies the signal of the start branch (S) of the switch, and its function is to protect the railway elements that are after this signal (i.e. elements that are in the detour branch and in the continue branch).

Some signals generated due to switches are shown in red colour in Figure 17:

- Sw03:*C124, S125 and H126*.
- D04:*C77, B78, S79 and H80*.
- Sw04:*C17, S128 and H129*.

![Figure 17](Figure4_zoom.png "Figure 17")

*Figure 17. Some signals due to line borders(L),buffer stops(T),rail joints (J), platforms(P),level crossings(X) and switches(S,H,C,B).*

The signals generte for all switches are shown in Figure 18.

![Figure 18](Figure4.jpg "Figure 18")

*Figure 18. All signals due to line borders(L),buffer stops(T),rail joints (J), platforms(P),level crossings(X) and switches(S,H,C,B).*

### F. Simplify signalling

The signal simplification process used by RNA relies on two main principles: i) vertical inheritance and ii) horizontal inheritance. Both principles are explained in [[1]](#references) in section "IV. SIGNALLING SIMPLIFICATION".

To simplify signals mark the configuration option "Simplify signals", as shown in Figure 19.

![Figure 19](config_5.PNG "Figure 19")

*Figure 19. Configuring RNA to simplify signalling.*

After the simplification only the appropriate signals are kept, as shown in Figure 20.

![Figure 20](Figure5.jpg "Figure 20")

*Figure 20. Signalling simplification.*

The simplification process was carried out according to the process described in section IV. SIGNALLING SIMPLIFICATION of [[1]](#references). Next, the signal simplification process in some network elements is shown:

- **Simplification by vertical inheritance**

    In Figure 21, vertical inheritance was applied when the B signals of the Sw03 and Sw04 were moved to the signals H126 y H129, respectively. These signals B were not created because of the RNA when analysing the switches, applying Algorithm 8 explained in section IV. SIGNALLING SIMPLIFICATION of [[1]](#references), literal A. 

- **Simplification by horizontal inheritance**

    In Figure 22, some of the simplified signals due to horizontal inheritance are C124, J39, C93, C127 and others. Signal C124 was deleted by RNA due it was nearby of signal T28, and have the same direction and orientation. The same situation occurs between signals J39 and S128; between signals C93 and J37; and between signals C127 and J36. In all cases, is applied Algorithm 9 (described in section IV. SIGNALLING SIMPLIFICATION of [[1]](#references)). This algorithm was designed to group nearby objects as one single object, and generating signals according to the leftmost and rightmost railway element in the new single object. 

    Note that signals C93 and C127 were deleted due to horizontal inheritance between signals J37 and J36, respectively. In this case, the priority of J37 and J36 were superior, as explained in section IV. SIGNALLING SIMPLIFICATION of [[1]](#references), literal B.

![Figure 21](Figure4_zoom.png "Figure 21")

*Figure 21. Clipping #1 of signalling simplification for vertical inheritance.*

![Figure 22](Figure5_zoom.png "Figure 22")

*Figure 22. Clipping #2 of signalling simplification for horizontal inheritance.*

The entire simplified sigals are shown in figure 23.

![Figure 23](Figure5.jpg "Figure 23")

*Figure 23. All signalling simplification.*

### G. Export a resulting railway layout description

Once the signalling is generated, it is necessary to establish the railway routes to create the railway interlocking table. A railway route is the simplest path between two consecutive signals in the same direction, using the same tracks (see [[1]](#references)).

#### G.1. Obtaining the interlocking table in Design4Rail

To obtain the interlocking table is necessary to use Design4Rail software to open the archive Example_2_B.railml" generated by RNA for this example, as shown in Figure 24.

![Figure 24](import_rail_aid_1.png "Figure 24")
![Figure 24](import_rail_aid_2.PNG "Figure 24")

*Figure 24. Import railml file.*

Once the file is opened, it will be possible to view the network and its elements, as in Figure 25.

![Figure 25](import_rail_aid_3.PNG "Figure 25")

*Figure 25. Example 4 network in Design4Rail Track Planner.*

In the menu "View" in Design4Rail Track Planner, select "Routes", as shown in Figure 26.

![Figure 26](import_rail_aid_4.png "Figure 26")

*Figure 26. View Routes*

Then Design4Rail Track Planner will display the interlocking table for this network. It is shown in Table 1.

*Table 1. Routes in Design4Rail*

![Table 1](import_rail_aid_5.PNG "Table 1")

### ***Note***

   To carry out this research work, we used the software Rail-AID developed by NEAT, and provided to us on July 2021. However, NEAT no longer supports this software. They upgrade to a new software named Desgin4Rail TrackPlanner application, whose functionalities are essentially the same as Rail-AID. Because of this reason, we recommended in the manuscript and the development of the examples available in this repository, the use of Design4Rail TrackPlanner. Users are notified, that Rail-AID and Design4Rail are not free software; therefore, appropriate licenses should be purchased for use. A trial version is sufficient to open and visualize the layouts of examples 2, 5, 6 y 7. However, to open and visualize examples 1, 3 y 4 a license should be purchased.

   Moreover, it is important to mention that when the RNA exports the railML file the Rail-AID software considers all these signals as a single aspect. This issue was notified by us to NEAT in March 2022, they acknowledged the notification, agreed that there is an error on their software and committed to fix this problem. However, this problem was never solved, and NEAT discontinued Rail-AID software, as explained above. This problem is not solved yet on Design4Rail, either. To get around this issue, the RNA creates N semaphores of one aspect and displays them one after the other, instead of creating one semaphore of N aspects. As a consequence of having N semaphores of one aspect the interlocking table has more routes than the scenario where there is one semaphore of N aspects. Therefore, to get the appropriate interlocking table corresponding to one semaphore of N aspects, use the procedure shown in section [G.1.](#g1-obtaining-the-interlocking-table-in-design4rail)

#### G.2. Original interlocking table

The structure of the original example is shown in Figure 27.

![Figure 27](4_A.png "Figure 27")

*Figure 27. Original example provided by RailMl.*

The signalling and the original interlocking table were designed by experts following the RailMl standard, and are shown in Table 2.

*Table 2. Original interlocking table for this example provided by RailMl*

| Route  | Entry | Exit | Switches | Platforms | Crossings | netElements |
|  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |
R_01  |  X19  |  S32  |  -  |  -  |  LC06-LC04  |  ne100-ne101
R_02  |  S32  |  S91  |  D09_N  |  -  |  -  |  ne101-ne912
R_03  |  C62  |  S04  |  SW02_R  |  -  |  -  |  ne104-ne384
R_04  |  B44  |  S04  |  SW02_N  |  -  |  -  |  ne110-ne384
R_05  |  S87  |  T08  |  -  |  -  |  -  |  ne114-ne102
R_06  |  B86  |  S87  |  D23_N  |  -  |  -  |  ne132-ne114
R_07  |  C89  |  C31  |  D20_N  |  -  |  -  |  ne132-ne912
R_08  |  S08  |  T03  |  D14_R + D15_R  |  -  |  -  |  ne290-ne111-ne377
R_09  |  C35  |  T01  |  D01_N  |  -  |  -  |  ne290-ne991
R_10  |  S09  |  C35  |  D14_N  |  -  |  -  |  ne292-ne290
R_11  |  S45  |  T01  |  D03_N + D01_R  |  -  |  -  |  ne295-ne288-ne991
R_12  |  B47  |  S40  |  D04_N  |  -  |  -  |  ne295-ne297
R_13  |  C43  |  S45  |  D04_N  |  -  |  -  |  ne297-ne295
R_14  |  S40  |  T02  |  SW03_N  |  -  |  -  |  ne297-ne995
R_15  |  S40  |  X15  |  Sw03_R + Sw04_R    |  -  |  LC02-LC01  |  ne297-ne997-ne996-ne98
R_16  |  S06  |  C35  |  D15_R + D14_R  |  -  |  -  |  ne377-ne111-ne290
R_17  |  S06  |  T10  |  D15_N  |  -  |  -  |  ne377-ne113
R_18  |  S04  |  S40  |  D04_R  |  -  |  -  |  ne384-ne297
R_19  |  C56  |  S58  |  D07_N  |  -  |  -  |  ne400-ne404
R_20  |  C56  |  S03  |  D07_R  |  -  |  -  |  ne400-ne407
R_21  |  S28  |  T04  |  Sw02_N    |  -  |  -  |  ne400-ne993
R_22  |  B52  |  S28  |  D07_N  |  -  |  -  |  ne404-ne400
R_23  |  S58  |  X16  |  D08_N + D05_R  |  -  |  LC02-LC01  |  ne404-ne61-ne99-ne98
R_24  |  S03  |  T11  |  D16_R  |  -  |  -  |  ne407-ne122
R_25  |  S10  |  S84  |  D18_R + D19_R  |  -  |  -  |  ne63-ne124-ne421
R_26  |  S10  |  S02  |  D18_N  |  -  |  -  |  ne63-ne65
R_27  |  C23  |  X16  |  D05_N  |  -  |  LC06-LC04  |  ne63-ne99-ne98
R_28  |  S11  |  C23  |  D18_N  |  -  |  -  |  ne65-ne63
R_29  |  C93  |  S95  |  D20_R + D21_R  |  -  |  -  |  ne912-ne131-ne465
R_30  |  C93  |  B86  |  D20_N  |  -  |  -  |  ne912-ne132
R_31  |  X15    |  S24    |  -  |   -   |   LC02   |  ne98-ne99
R_32  |  S07  |  S68  |  D01_N  |  -  |  -  |  ne991-ne290
R_33  |  B27  |  C56  |  Sw02_N    |  -  |  -  |  ne993-ne400
R_34  |  B39  |  C43  |  SW03_N  |  -  |  -  |  ne995-ne297
R_35  |  S24  |  S80  |  D05_N  |  -  |  -  |  ne99-ne63
R_36  |  X20  |  S11  |  SW01_N  |  -  |  (LC05-LC03) - (LC06-LC04)  |  ne100-ne992-ne65
R_37  |  X20  |  C56  |  Sw01_R + Sw02_R    |  -  |  (LC05-LC03) - (LC06-LC04)  |  ne100-ne992-ne994-ne400
R_38  |  S32  |  C59  |  D09_R + D10_N  |  -  |  -  |  ne101-ne910-ne130
R_39  |  S32  |  B60  |  D09_R + D10_R  |  -  |  -  |  ne101-ne910-ne135
R_40  |  S01  |  X20  |  D10_N + D9_R  |  -  |  LC06-LC04  |  ne130-ne910-ne101-ne100
R_41  |  B98  |  X20  |  D10_R + D09_R  |  -  |  LC05-LC03  |  ne135-ne910-ne101-ne100
R_42  |  S08  |  X15  |  D14_N + SW04_N  |  -  |  LC02-LC01  |  ne290-ne292-ne996-ne98
R_43  |  S28  |  X29  |  Sw02_R + Sw01_R    |  -  |  (LC05-LC03) - (LC06-LC04)  |  ne400-ne994-ne992-ne100
R_44  |  S02  |  X19  |  SW01_N  |  -  |  (LC05-LC03) - (LC06-LC04)  |  ne65-ne992-ne100
R_45  |  C31  |  X20  |  D09_N  |  -  |  LC06-LC04  |  ne912-ne101-ne100
R_46  |  X16    |  B67    |  Sw04_N    |  -  |  -  |  ne98-ne996-ne292
R_47  |  S16    |  S43    |  Sw03_R + Sw04_R    |  -  |  -  |  ne98-ne996-ne997-ne297
R_48  |  S07  |  B44  |  D01_R + D03_R  |  -  |  -  |  ne991-ne288-ne110
R_49  |  S07  |  B47  |  D01_R + D03_N  |  -  |  -  |  ne991-ne288-ne295
R_50  |  S24  |  B57  |  D05_R + D08_R  |  -  |  -  |  ne99-ne61-ne123
R_51  |  S24  |  B52  |  D05_R + D08_N  |  -  |  -  |  ne99-ne61-ne404
R_52  |  B63  |  T01  |  D03_R + D01_R  |  -  |  -  |  ne110-ne288-ne991
R_53  |  C74  |  S76  |  D16_R  |  -  |  -  |  ne122-ne407
R_54  |  B58  |  S76  |  D16_N  |  -  |  -  |  ne123-ne407
R_55  |  B75  |  X16  |  D08_R + D05_R  |  -  |  LC02-LC01  |  ne123-ne61-ne99-ne98
R_56  |  S99  |  S87  |  D12_S + D23_R  |  -  |  -  |  ne127-ne129-ne114
R_57  |  S99  |  T06  |  D12_T  |  -  |  -  |  ne127-ne450
R_58  |  C59  |  S87  |  D12_T + D23_R  |  -  |  -  |  ne130-ne129-ne114
R_59  |  C59  |  T06  |  D12_S  |  -  |  -  |  ne130-ne450
R_60  |  C97  |  S99  |  D24_R  |  -  |  -  |  ne134-ne127
R_61  |  B60  |  S99  |  D24_N  |  -  |  -  |  ne135-ne127
R_62  |  C43  |  C46  |  D04_R  |  -  |  -  |  ne297-ne384
R_63  |  C46  |  T09  |  Sw02_R  |  -  |  -  |  ne384-ne104
R_64  |  C46  |  B63  |  SW02_N  |  -  |  -  |  ne384-ne110
R_65  |  S03  |  B75  |  D16_N  |  -  |  -  |  ne407-ne123
R_66  |  S76  |  S28  |  D07_R  |  -  |  -  |  ne407-ne400
R_67  |  B83  |  T12  |  -  |  -  |  -  |  ne126
R_68  |  B90  |  C89  |  -  |  -  |  -  |  ne132
R_69  |  B94  |  T13  |  -  |  -  |  -  |  ne133
R_70  |  S68  |  S08  |  -  |  -  |  -  |  ne290
R_71  |  B67  |  S09  |  -  |  -  |  -  |  ne292
R_72  |  S84  |  H85  |  -  |  -  |  -  |  ne421
R_73  |  H85  |  T05  |  -  |  -  |  -  |  ne421
R_74  |  S95  |  H96  |  -  |  -  |  -  |  ne465
R_75  |  H96  |  T07  |  -  |  -  |  -  |  ne465
R_76  |  S80  |  S10  |  -  |  -  |  -  |  ne63

#### G.3. Generated interlocking table

The result of the automatic process carried by the RNA is the intelocking table shown in Table 3. This result is consistent with Table 1 shown in subsection [G.2.](#g2-original-interlocking-table) Original interlocking table.

*Table 3. Interlocking table obtain through RNA when the option "One-direction only" is marked.*

| Route  | Entry | Exit | Switches | Platforms | Crossings | netElements |
|  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |
R_01  |  X56  |  S67  |  -  |  -  |  LC06-LC04  |  ne100-ne101
R_02  |  S67  |  S112  |  D09_N  |  -  |  -  |  ne101-ne912
R_03  |  T14  |  B78  |  SW02_R  |  -  |  -  |  ne104-ne384
R_04  |  B75  |  B78  |  SW02_N  |  -  |  -  |  ne110-ne384
R_05  |  J48  |  T11  |  -  |  -  |  -  |  ne114-ne102
R_06  |  J46  |  L29  |  D03_N  |  -  |  -  |  ne132-ne114
R_07  |  J47  |  J45  |  D20_N  |  -  |  -  |  ne132-ne912
R_08  |  S94  |  T03  |  D14_R + D15_R  |  -  |  -  |  ne290-ne111-ne377
R_09  |  J35  |  T01  |  D01_N  |  -  |    |  ne290-ne991
R_10  |  J37  |  J35  |  D14_N  |  -  |  -  |  ne292-ne290
R_11  |  C74  |  T01  |  D03_N + D01_R  |  -  |  -  |  ne295-ne288-ne991
R_12  |  C77  |  S125  |  D04_N  |  -  |  -  |  ne295-ne297
R_13  |  S79  |  C74  |  D04_N  |  -  |  -  |  ne297-ne295
R_14  |  S125  |  T27  |  SW03_N  |  -  |  -  |  ne297-ne995
R_15  |  S125  |  L30  |  SW03_R + SW04_R  |  -  |  -  |  ne297-ne997-ne996-ne98
R_16  |  T04  |  J35  |  D15_R + D14_R  |  -  |  -  |  ne377-ne111-ne290
R_17  |  T04  |  T15  |  D15_N  |  -  |  -  |  ne377-ne113
R_18  |  B78  |  S125  |  D04_R  |  -  |  -  |  ne384-ne297
R_19  |  S82  |  C84  |  D07_N  |  -  |  -  |  ne400-ne404
R_20  |  S82  |  S101  |  D07_R  |  -  |  -  |  ne400-ne407
R_21  |  S91  |  T25  |  SW02_N  |  -  |  -  |  ne400-ne993
R_22  |  C81  |  S91  |  D07_N  |  -  |  -  |  ne404-ne400
R_23  |  C84  |  X51  |  D08_N + D05_R  |  -  |  LC02-LC01  |  ne404-ne61-ne99-ne98
R_24  |  S101  |  T17  |  D16_R  |  -  |  -  |  ne407-ne122
R_25  |  S103  |  T05  |  D18_R + D19_R  |  -  |  -  |  ne63-ne124-ne421
R_26  |  S103  |  C121  |  D18_N  |  -  |  -  |  ne63-ne65
R_27  |  C62  |  X51  |  D05_N  |  -  |  LC02-LC01  |  ne63-ne99-ne98
R_28  |  C102  |  C62  |  D18_N  |  -  |  -  |  ne65-ne63
R_29  |  S112  |  T09  |  D20_R + D21_R  |  -  |  -  |  ne912-ne131-ne465
R_30  |  S112  |  J46  |  D20_N  |  -  |  -  |  ne912-ne132
R_31  |  X50  |  S63  |  -  |  -  |  LC02-LC01  |  ne98-ne99
R_32  |  S71  |  S94  |  D01_N  |  -  |  -  |  ne991-ne290
R_33  |  T26  |  S82  |  SW02_N  |  -  |  -  |  ne993-ne400
R_34  |  T28  |  S79  |  SW03_N  |  -  |  -  |  ne995-ne297
R_35  |  S63  |  S103  |  D05_N  |  -  |  -  |  ne99-ne63
R_36  |  X55  |  S122  |  -  |  -  |  LC05-LC03  |  ne100-ne992
R_37  |  J43  |  X57  |    |    |  LC06-LC04  |  ne101-ne100
R_38  |  S67  |  S89  |  D09_R  |  -  |  -  |  ne101-ne910
R_39  |  B85  |  S91  |  D16_N + D07_R  |  -  |  -  |  ne123-ne407-ne400
R_40  |  S119  |  J43  |  D24_N + D10_R + D09_R  |  -  |  -  |  ne127-ne135-ne910-ne101
R_41  |  C87  |  J43  |  D10_N + D09_R  |  -  |  -  |  ne130-ne910-ne101
R_42  |  S76  |  B75  |  D03_R  |  -  |  -  |  ne288-ne110
R_43  |  S76  |  C77  |  D03_N  |  -  |  -  |  ne288-ne295
R_44  |  S94  |  J36  |  D14_N  |  -  |  -  |  ne290-ne292
R_45  |  J36  |  L30  |  SW04_N  |  -  |  -  |  ne292-ne996-ne98
R_46  |  S91  |  L32  |  SW02_R + SW01_R  |  -  |  -  |  ne400-ne994-ne992
R_47  |  S86  |  B85  |  D08_R  |  -  |  -  |  ne61-ne123
R_48  |  S86  |  C81  |  D08_N  |  -  |  -  |  ne61-ne404
R_49  |  C121  |  L32  |  SW01_N  |  -  |  -  |  ne65-ne992
R_50  |  S89  |  B88  |  D10_R  |  -  |  -  |  ne910-ne135
R_51  |  J45  |  J43  |  D09_N  |  -  |  -  |  ne912-ne101
R_52  |  X51  |  S128  |  -  |  -  |  -  |  ne98-ne996
R_53  |  S71  |  S76  |  D01_R  |  -  |  -  |  ne991-ne288
R_54  |  L32  |  L31  |  -  |  -  |  -  |  ne992-ne100
R_55  |  S122  |  C102  |  SW01_N  |  -  |  -  |  ne992-ne65
R_56  |  S122  |  S82  |  SW01_R + SW02_R  |  -  |  -  |  ne992-ne994-ne400
R_57  |  S128  |  J37  |  SW04_N  |  -  |  -  |  ne996-ne292
R_58  |  S128  |  S79  |  SW04_R + SW03_R  |  -  |  -  |  ne996-ne997-ne297
R_59  |  S63  |  S86  |  D05_R  |  -  |  -  |  ne99-ne61
R_60  |  T18  |  S91  |  D16_R + D07_R  |  -  |  -  |  ne122-ne407-ne400
R_61  |  T24  |  L29  |  D24_R + D12_S + D23_R  |  -  |  -  |  ne134-ne127-ne129-ne114
R_62  |  T24  |  T07  |  D24_R + D12_T  |  -  |  -  |  ne134-ne127-ne450
R_63  |  B88  |  L29  |  D24_N + D12_S + D23_R  |  -  |  -  |  ne135-ne127-ne129-ne114
R_64  |  B88  |  T07  |  D24_N + D12_T  |  -  |  -  |  ne135-ne127-ne450
R_65  |  S79  |  T13  |  D04_R + SW02_R  |  -  |  -  |  ne297-ne384-ne104
R_66  |  S79  |  T01  |  D04_R + SW02_N +D03_R + D01_R  |  -  |  -  |  ne297-ne384-ne110-ne288-ne991
R_67  |  S101  |  X51  |  D08_R + D05_R  |  -  |  LC02-LC01  |  ne407-ne123-ne61-ne99-ne98
R_68  |  S89  |  L29  |  D10_N + D12_T + D23_R  |  -  |  -  |  ne910-ne130-ne129-ne114
R_69  |  S89  |  T07  |  D10_N + D12_S  |  -  |  -  |  ne910-ne130-ne450
R_70  |  L31  |  X54  |  -  |  -  |  LC05-LC03  |  ne100
R_71  |  X54  |  X56  |  -  |  -  |  -  |  ne100
R_72  |  X57  |  X55  |  -  |  -  |  (LC05-LC03) - (LC06-LC04)  |  ne100
R_73  |  T12  |  S109  |  -  |  -  |  -  |  ne102-ne114
R_74  |  T16  |  T03  |  D15_N  |  -  |  -  |  ne113-ne377
R_75  |  L29  |  J48  |  -  |  -  |  -  |  ne114
R_76  |  S109  |  J47  |  D23_N  |  -  |  -  |  ne114-ne132
R_77  |  S109  |  S119  |  D23_R + D12_S  |  -  |  -  |  ne115-ne129-ne127

#### G.3.1. One-directional and bidirectional tracks

RNA can consider tracks as bidirectional, while the original layout has only one-directional track. This feature is activated by mismarking the "One direction only" option, as shown in Figure 28.

![Figure 28](config_5.PNG "Figure 28")

*Figure 28. Produce routes considering bidirectional tracks*

In this way the extra routes shown in Table 4 are obtained, where routes 78 to 89 are the opposite of routes 1 to 5. This extra routes does not affect safety. Moreover, departure signals are considered for line borders and buffer stops for extra protection.

*Table 4. Interlocking table obtain through RNA when the option "One direction only" is mismarked.*

| Route  | Entry | Exit | Switches | Platforms | Crossings | netElements |
|  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |
R_78  |  S109  |  C87  |  D23_R + D12_T  |  -  |  -  |  ne115-ne129-ne130
R_79  |  T20  |  T05  |  D19_N  |  -  |  -  |  ne126-ne421
R_80  |  S119  |  T23  |  D24_R  |  -  |  -  |  ne127-ne134
R_81  |  T22  |  T09  |  D21_N  |  -  |  -  |  ne133-ne465
R_82  |  T06  |  C62  |  D19_R + D18_R  |  -  |  -  |  ne421-ne124-ne63
R_83  |  T06  |  T19  |  D19_N  |  -  |  -  |  ne421-ne126
R_84  |  T08  |  S119  |  D12_T  |  -  |  -  |  ne450-ne127
R_85  |  T08  |  C87  |  D12_S  |  -  |  -  |  ne450-ne130
R_86  |  T10  |  J45  |  D21_R + D20_R  |  -  |  -  |  ne465-ne131-ne912
R_87  |  T10  |  T21  |  D21_N  |  -  |  -  |  ne465-ne133
R_88  |  L30  |  X50  |  -  |  -  |  -  |  ne98
R_89  |  T02  |  S71  |  -  |  -  |  -  |  ne991

Table 4 shows the additional routes, considering bidirectional tracks. Routes 78 to 89 are the opposite of routes 1 to 77. So it does not affect safety, RNA always considers every possible route in the layout. Moreover, departure signals are considered for line borders and buffer stops for extra protection.

#### G.3.2. Minimum distance parameter

As explained in literal B of section "IV. SIGNALING SIMPLIFICATION" in [[1]](#references), more than two railway elements can be combined if they are close enough. The threshold distance to determine if this combination must be done is a configuration parameter of RNA, named MIN_DISTANCE (minimum distance). As shown in Algorithms 8, 9, and 10 in [[1]](#references), this parameter is essential to locate, relocate and simplify signals. Because of integrity software reasons, this parameter should be between 300 and 500. For default, this value is 300. Figure 29 shows the parameter configuration in the GUI of RNA. 

![Figure 29](minimum_distance_parameter.png "Figure 29")

*Figure 29. Minimum distance parameter configuration*

#### G.3.3. Fixed length parameter

The fixed length parameter is necessary to allocate the departure signals, which maintains the trains in the network until the next network approves the movement. These signals allow trains to move outside the network without restrictions only if the track is not long enough (fixed length). RNA could easily be adapted to different criteria and regulations, thanks to this parameter. As shown in Algorithms 3, and 4 in [[1]](#references). Configuration of the fixed length parameter in RNA as shown in Figure 22. Because of integrity software reasons, this parameter should be between 300 and 500. For default, this value is 200. Figure 30 shows the parameter configuration in the GUI of RNA.

![Figure 30](fixed_length_parameter.jpeg "Figure 30")

*Figure 30. Fixed length parameter configuration*

## References

[1] M. N. Menendez, S. Germino, L. Díaz-Charris, and A. Lutenberg, Automatic Railway Signalling Generation for Railways Systems Described on Railway Markup Language (railML). 
