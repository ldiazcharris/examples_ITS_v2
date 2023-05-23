# Example_7
## Description

Name: Complex switches II

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

Figure 2 shows the railway network without signalling. The user will need the Design4Rail Horizon Software Suite Track Planner application and import the archive "Example_7.railml" to visualise the railway network used in this example. 

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
Analysing railML object
 Analysing graph
ne1 [-770, -30] [260, -30] >>    
ne31 [554, 480] [1190, 480] >>   
ne32 [554, 480] [1460, 957] >>   
ne40 [260, -30] [554, 480] >>    
ne41 [260, -30] [1040, -420] >>  
ne42 [1040, -420] [1730, -420] >>
ne43 [1040, -420] [440, -420] << 
 The network is connected
~~~

*Console Output 1. Step B railway elements.*

In this example, the Console Output 1 shows that the program can identify the nodes and their directions. Consol Output 1 has, for example, this line: ne43 [1040, -420] [440, -420] <<, it indicates the name of the netElement (ne43), the position (origin [1040, -420] and end point [440, -420]) of the net element, and the direction (<<, to the left in this case, but in other example it could have been to the right: >>). If compare this Console Output 1 with Figure 2, and analysing each "netElement", all elements are coincident. The same analysis for: ne1, ne31, ne32, ne40, ne41 and ne42.

### C and D. Infrastructure analysis and CDL zones detection

The process of analysing the infrastructure and detecting CDL zones allows identifying the position of each infrastructure element in the network: platforms, curves, level crossings, buffer stops, derailers, lines, operational points, signals, switches, tracks and detection elements (axle counters, rail joints and track circuits).

In section "II. RAILWAY NETWORK ANALYSER DESIGN" literal C of [[1]](#references), it is shown Algorithm 2, which explains the process of analysing the network; and in the same section but in literal D, it is explained the process used to detect CDL zones.

The result of this step is shown in Console Output 2 and Figure 3.

~~~
Analysing infrastructure --> Infrastructure.RNA
 Detecting Danger --> Safe_points.RNA
  ne1 has a Middle point @ [-255.0, -30]
  ne31 has a Middle point @ [872.0, 480]
  ne32 has a Curve(2 lines) @ [[830, 957]]
  ne41 has a Curve(2 lines) @ [[650, -30]]
  ne42 has a Middle point @ [1385.0, -420]
  ne43 has a Middle point @ [740.0, -420]
~~~

*Console Output 2. Infraestructure analysis and CDL zone detection.*

![Figure 3](step_C_and_D_2.PNG "Figure 3")

*Figure 3. Infrastructure analysis and CDL zones detection: GUI Output.*

Figure 4 shows these elements.

![Figure 4](step_C_and_D_graphic.jpg "Figure 4")

*Figure 4. Infrastructure analysis and CDL zones detection: Layout.*

### E. Generate signalling

To obtain an analysis for each network element in the program configurations (view Figure 5), select only the options you want.

![Figure 5](config_options.png "Figure 5")

*Figure 5. Configuration options of RNA.*

Below, in subsections E.1, E.2, E.3, and E.4, you will find the sequence of configurations used to analyze, step by step, the railway in this example.

#### E.1. Signals generated due to line borders(L) and buffer stops(T)

The configuration of the RNA GUI application needed for this step of the analysis is shown in Figure 6.

![Figure 6](config_1.png "Figure 6")

*Figure 6. Configuring RNA to obtain signals for line borders(L) and buffer stops(T).*

Signals are enumerated since 00 with a prefix letter to indicate which element generates them. BufferStops and LineBorders signals start with T and L, respectively. In Figure 7, we can visualise the signals generated by applying algorithm 3, explained in [[1]](#references) section "III. SIGNALLING GENERATION".

In red letters, automatically added signals are shown.

The RNA allocates signals close to the buffer stops:

-- Stop: *T01*, *T05*, *T07*, *T09*

-- Departure: *T02*, *T04*, *T06*, *T08*, *T10*

The RNA does not allocate any signal close to the line borders because this layout has zero (0) line borders.

![Figure 7](Figure1.jpg "Figure 7")

*Figure 7. Signals due to line borders(L) and buffer stops(T).*

#### E.2. Signals generated due to line borders(L), buffer stops(T) and rail joints (J)

The signals for rail joints are named J and have a consecutive number of signals.

The configuration of the RNA GUI application needed for this step of the analysis is shown in Figure 8.

![Figure 8](config_2.png "Figure 8")

*Figure 8. Configuring RNA to obtain signals for line borders(L), buffer stops(T) and rail joints (J).*

The algorithm does not assign signalling at the beginning and end of each track because this network does not have rail joints as shown in Figure 9.

![Figure 9](Figure2.jpg "Figure 9")

*Figure 9. Signals due to line borders(L), buffer stops(T) and rail joints (J).*

#### E.3. Signals generated due to line borders(L), buffer stops(T),rail joints (J), platforms(P) and level crossings(X)

The signals for platforms are named P, and signals for level crossings are named X. A consecutive number of signals is assigned for each type of signalling.

The configuration of the RNA GUI application needed for this step of the analysis is shown in Figure 10.

![Figure 10](config_3.png "Figure 10")

*Figure 10. Configuring RNA to obtain signals for line borders(L),buffer stops(T),rail joints (J), platforms(P) and level crossings(X).*

Notice that RNA can be configured to avoid adding duplicate signals when the level crossing and the platform are close together, as discussed in [[1]](#references), and therefore, the signalling between them is unnecessary. However, this configuration is a special parameter in RNA. For furthermore information about this, see section [G.3.1.2.](#g32-minimum-distance-parameter) 

It is necessary to introduce signals before the train reaches the level crossing as explained in Algorithm 5, explained in [[1]](#references) section "III. SIGNALLING GENERATION".

Also, it is necessary to have a departure signal after the platform. This logic is implemented using Algorithm 6, explained in [[1]](#references) section "III. SIGNALLING GENERATION".

In red letters, the signals Generated due level crossings and platforms are shown in Figure 11.

![Figure 11](Figure3.jpg "Figure 11")

*Figure 11. Signals due to line borders(L),buffer stops(T),rail joints (J), platforms(P) and level crossings(X).*

#### E.4. Signals generated due to line borders(L),buffer stops(T),rail joints (J), platforms(P),level crossings(X) and switches(S,H,C,B)

Figure 6 shows the configuration of the RNA GUI application needed for this step of analysis.

![Figure 12](config_4.png "Figure 12")

*Figure 12. Configuring RNA to obtain signals for line borders(L),buffer stops(T),rail joints (J), platforms(P),level crossings(X) and switches(S,H,C,B).*

The signals for switches are named based on the point they want to protect: S for Starting branch, C for the Continue branch and B for the Detour branch. There are also signals whose name starts with H that are not explicitly protecting the starting branch, the continue branch or the detour branch of a switch. These H signals are explained in [[1]](#references) section "III. SIGNALLING GENERATION" in literal E, where a manoeuvre signal numbered with H is always added plus the corresponding numbering sequence by Algorithm 7. This manoeuvre signal always accompanies the signal of the start branch (S) of the switch, and its function is to protect the railway elements that are after this signal (i.e. elements that are in the detour branch and in the continue branch).

Signals generated for Example 7 are shown in red letters in Figure 13:

- Sw18:*S14, C13, B18, H15, H16*.
- Sw14:*C11 and B12*.
- Sw19:*S19, H20. C17*.

![Figure 13](Figure4.jpg "Figure 13")

*Figure 13. Signals due to line borders(L),buffer stops(T),rail joints (J), platforms(P),level crossings(X) and switches(S,H,C,B).*

### F. Simplify signalling

The signal simplification process used by RNA relies on two main principles: i) vertical inheritance and ii) horizontal inheritance. Both principles are explained in [[1]](#references) in section "IV. SIGNALLING SIMPLIFICATION".

To simplify signals is needed that, mark the configuration option "Simplify signals", as shown in Figure 14.

![Figure 14](config_5.png "Figure 14")

*Figure 14. Configuring RNA to simplify signalling.*

After the simplification only the appropriate signals are kept, as shown in Figure 15.

![Figure 15](7_B.png "Figure 15")

*Figure 15. Signalling simplification.*

The simplification process was carried out according to the process described in section IV. SIGNALLING SIMPLIFICATION of [[1]](#references), as follows:

- **Simplification by vertical inheritance**

    Vertical inheritance was applied when the B signals between Sw10 and Sw14 were moved to the signals H15 y H16, respectably. These signals B were not created, because the RNA applied Algorithm 8 explained in section IV. SIGNALLING SIMPLIFICATION of [[1]](#references), literal A. It also moves signal C for Sw10 to H20. 

- **Simplification by horizontal inheritance**

    The simplified signals due to horizontal inheritance are follows: C13, S19 amd B12. Signal L03 and S19 were deleted due this was nearby of signal H20, with the same direction and orientation. The same situation occurs between signals B12 and T04. In all cases, is applied Algorithm 9 (described in section IV. SIGNALLING SIMPLIFICATION of [1]). This algorithm was designed to avoid collisions by considering nearby objects as one single object, and generating signals according to the leftmost and rightmost railway element in the new single object. 

    The priority of the surviving signals were higher than the replaced signals, as explained in section IV. SIGNALLING SIMPLIFICATION of [1], literal B. 

### G. Export a resulting railway layout description

Once the signalling is generated, it is necessary to establish the railway routes to create the railway interlocking table. A railway route is the simplest path between two consecutive signals in the same direction, using the same tracks (see [[1]](#references)).

<a name="G.1"></a>
#### G.1. Obtaining the interlocking table in Design4Rail

To obtain the interlocking table is necessary to use Design4Rail software to open the archive Example_2_B.railml" generated by RNA for this example, as shown in Figure 16.

![Figure 16](import_rail_aid_1.png "Figure 16")
![Figure 16](import_rail_aid_2.png "Figure 16")

*Figure 16. Import railml file.*

Once the file is opened, it will be possible to view the network and its elements, as in Figure 17.

![Figure 17](import_rail_aid_3.PNG "Figure 17")

*Figure 17. Example 2 network in Design4Rail Track Planner.*

In the menu "View" in Design4Rail Track Planner, select "Routes", as shown in Figure 18.

![Figure 18](import_rail_aid_4.png "Figure 18")

*Figure 18. View Routes*

Then Design4Rail Track Planner will display the table of routes for this network. It is shown in Table 1.

*Table 1. Routes in Design4Rail*

![Table 1](import_rail_aid_5.png "Table 1")

### ***Note***

   To carry out this research work, we used the software Rail-AID developed by NEAT, and provided to us on July 2021. However, NEAT no longer supports this software. They upgrade to a new software named Desgin4Rail TrackPlanner application, whose functionalities are essentially the same as Rail-AID. Because of this reason, we recommended in the manuscript and the development of the examples available in this repository, the use of Design4Rail TrackPlanner. Users are notified, that Rail-AID and Design4Rail are not free software; therefore, appropriate licenses should be purchased for use. A trial version is sufficient to open and visualize the layouts of examples 2, 5, 6 y 7. However, to open and visualize examples 1, 3 y 4 a license should be purchased.

   Moreover, it is important to mention that when the RNA exports the railML file the Rail-AID software considers all these signals as a single aspect. This issue was notified by us to NEAT in March 2022, they acknowledged the notification, agreed that there is an error on their software and committed to fix this problem. However, this problem was never solved, and NEAT discontinued Rail-AID software, as explained above. This problem is not solved yet on Design4Rail, either. To get around this issue, the RNA creates N semaphores of one aspect and displays them one after the other, instead of creating one semaphore of N aspects. As a consequence of having N semaphores of one aspect the interlocking table has more routes than the scenario where there is one semaphore of N aspects. Therefore, to get the appropriate interlocking table corresponding to one semaphore of N aspects, use the procedure shown in section [G.1.](#g1-obtaining-the-interlocking-table-in-design4rail)

#### G.2. Original interlocking table

Figure 19 shows the structure of the original example. 

![Figure 19](7_A.png "Figure 19")

*Figure 19. Original example provided by RailMl*

The signalling and the original interlocking table were designed by experts following the RailMl standard, and are shown in Table 2.

*Table 2. Original interlocking table for this example provided by RailMl*

| Route  | Entry | Exit | Switches | Platforms | Crossings | netElements |
|  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |
| R_01 |  S01  |  S02  | Sw18_N | - | - | ne01-ne41 |
| R_02 |  S01  |  S06  | Sw14_N + Sw18_R | - | - | ne01-ne40-ne32 |
| R_03 |  S01  |  S07  | Sw14_R + Sw18_R | - | - | ne01-ne40-ne31 |
| R_04 |  S03  |  S09  | Sw19_N | - | - | ne42-ne43 |
| R_05 |  S03  |  S10  | Sw18_N + Sw19_R | - | - | ne42-ne41-ne01 |
| R_06 |  S02  |  S08  | Sw19_R | - | - | ne41-ne42 |
| R_07 |  S04  |  S10  | Sw14_R + Sw18_R | - | - | ne31-ne40-ne01 |
| R_08 |  S05  |  S10  | Sw14_N + Sw18_R | - | - | ne32-ne40-ne01 |

#### G.3. Generated interlocking table

The result of the automatic process carried by the RNA is the intelocking table shown in Table 3. This result is consistent with Table 1 shown in subsection [G.2.](#g2-original-interlocking-table) Original interlocking table.

*Table 3. Interlocking table obtain through RNA when the option "One-direction only" is marked.*

| Route  | Entry | Exit | Switches | Platforms | Crossings | netElements |
|  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |
| R_01 |  S14  |  B18  | Sw18_N | - | - | ne01-ne41 |
| R_02 |  S14  |  T05  | Sw14_N + Sw18_R | - | - | ne01-ne40-ne32 |
| R_03 |  S14  |  T03  | Sw14_R + Sw18_R | - | - | ne01-ne40-ne31 |
| R_04 |  S19  |  T09  | Sw19_N | - | - | ne42-ne43 |
| R_05 |  S19  |  T01  | Sw18_N + Sw19_R | - | - | ne42-ne41-ne01 |
| R_06 |  B18  |  T07  | Sw19_R | - | - | ne41-ne42 |
| R_07 |  T04  |  T01  | Sw14_R + Sw18_R | - | - | ne31-ne40-ne01 |
| R_08 |  C11  |  T01  | Sw14_N + Sw18_R | - | - | ne32-ne40-ne01 |

Routes 1 to 8 are equivalente in both interlocking tables.


#### G.3.1. One-directional and bidirectional tracks

RNA can consider tracks as bidirectional, while the original layout has only one-directional track. This feature is activated by mismarking the "One direction only" option, as shown in Figure 20.

![Figure 20](one_direction_mismarked.png "Figure 20")

*Figure 20. Produce routes considering bidirectional tracks*

In this way the extra routes shown in Table 4 are obtained, where routes 6 to 10 are the opposite of routes 1 to 5. This extra routes does not affect safety. Moreover, departure signals are considered for line borders and buffer stops for extra protection.

*Table 4. Interlocking table obtain through RNA when the option "One direction only" is mismarked.*

| Route  | Entry | Exit | Switches | Platforms | Crossings | netElements |
|  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |
| R_09 |  T02  |  S14  | - | - | - | ne01 |
| R_10 |  T06  |  C11  | - | - | - | ne32 |
| R_11 |  T08  |  S19  | - | - | - | ne42 |
| R_12 |  T10  |  T07  | Sw19_N | - | - | ne43-ne42 |

Table 4 shows the additional routes, considering bidirectional tracks. Routes 1 to 8 are the same in both interlocking tables, but RNA considers tracks as bidirectional, while the original layout has only one direction per track. Routes 9 to 11 are for used to allow stopped trains to move close to the main signals S14, S19 and C11. Route 12 is the opposite of route of route 4. So it does not affect safety, RNA always considers every possible route in the layout. Moreover, departure signals (T02, T06, T08 and T10) are considered for line borders and buffer stops for extra protection.

#### G.3.2. Minimum distance parameter

As explained in literal B of section "IV. SIGNALING SIMPLIFICATION" in [[1]](#references), more than two railway elements can be combined if they are close enough. The threshold distance to determine if this combination must be done is a configuration parameter of RNA, named MIN_DISTANCE (minimum distance). As shown in Algorithms 8, 9, and 10 in [[1]](#references), this parameter is essential to locate, relocate and simplify signals. Because of integrity software reasons, this parameter should be between 300 and 500. For default, this value is 300. Figure 22 shows the parameter configuration in the GUI of RNA. 

![Figure 22](minimum_distance_parameter.png "Figure 22")

*Figure 22. Minimum distance parameter configuration*

#### G.3.3. Fixed length parameter

The fixed length parameter is necessary to allocate the departure signals, which maintains the trains in the network until the next network approves the movement. These signals allow trains to move outside the network without restrictions only if the track is not long enough (fixed length). RNA could easily be adapted to different criteria and regulations, thanks to this parameter. As shown in Algorithms 3, and 4 in [[1]](#references). Configuration of the fixed length parameter in RNA as shown in Figure 23. Because of integrity software reasons, this parameter should be between 300 and 500. For default, this value is 200. Figure 23 shows the parameter configuration in the GUI of RNA.

![Figure 23](fixed_length_parameter.jpeg "Figure 23")

*Figure 23. Fixed length parameter configuration*

## References

[1] M. N. Menendez, S. Germino, L. Díaz-Charris, and A. Lutenberg, Automatic Railway Signalling Generation for Railways Systems Described on Railway Markup Language (railML). 
