# Example 2

## Description

Name: SimpleExample.railAID

This exaple was mencioned in the wrote paper titled: "Automatic Railway Signalling Generation for Railways Systems Described on Railway Markup Language (railML)". Henceforth, when refers to the paper, it's do as [1].

## Analysis principles

The signalling generation process used in this work was designed following signalling principles detailed in [1] in section "I. INTRODUCTION".

## Step by step

The following is the general methodology or "step by step" followed for the analysis of a railway network with the approach of this work [1].

A. Import the railway layout description.

B. Define a graph network to associate the railway elements.

C. Infraestructure analysis

D. Detect CDL zones.

E. Generate signalling.

F. Simplify signalling.

G. Export a resulting railway layout description.

Each step is explained below.

### A. Import the railway layout description

After having installed the RNA program according to the steps shown in the [Link](https://github.com/GICSAFePhD/Layouts) in secction "Usage", run the Python archive "main_GUI.py". This action produce the below program output:

![Figure 1](select_example.png "Figure 1")
*Figure 1. Select example*

The necessary information to define the graph network is distributed across several sections of the railML file, specifically inside netElements (nodes) and netRelations (edges) items found in the class Infrastructure/Topology.

In Figure 2 it can see the railway network without signalling. This figure not will show by the program, it is a visual help for the user of this manual example. The user will need the Rail-AID program and import the archive "Example_2.railml" to visualize the railway network for this example.

![Figure 2](Figure0.svg "Figure 2")
*Figure 2. Railway network without signalling.*

### B. Define a graph network to associate the railway elements

This step allows to determine that the provided file's network connections are consistent. It also allows verifying the address, position and interconnection of each node in the network.

In [1] in section "II. RAILWAY NETWORK ANALYZER DESIGN" in literal B, it can see Algorithm 1, that explain the process to analyses the network.

The result of this step is show in Console Output 1:

~~~
#################### Starting Railway Network Analyzer ####################
Reading .railML file
Creating railML object
Analyzing railML object
 Analyzing graph
ne14 [-1521, 450] [-560, 450] True >> False
ne15 [-1521, 300] [-560, 450] True >> False
ne16 [-560, 450] [516, 450] True >> False
ne17 [516, 450] [666, 300] True >> False
ne18 [516, 450] [1521, 450] True >> False
ne19 [666, 300] [28, 300] False << True
ne20 [666, 300] [1521, 300] True >> False
 The network is connected
~~~

*Console Output 1. Step B railway elements.*

In this example, is possible to view that the program can indentify the nodes and her directions viwed in Figure 2: ne14, ne15, ne16, ne17, ne18, ne19 and ne20.

### C and D. Infraestructure analysis and CDL zones detection

The process to analyses the infracestructure and detect CDL zones produce a one result: identify  the existence and position  of each infraestructure elements in the network: platforms, curves, level crossings,  buffer stops, derailers, lines,  operational points, signals, switches, tracks and detection elements (axle counters, rail joints and track circuits).

However, in [1] in section "II. RAILWAY NETWORK ANALYZER DESIGN" in literal C, it can see Algorithm 2, that explain the process to analyses the network; and in the same section but in literal D it explained the process for detect CDL zonees.

The result of this step is show in Console Output 2 and Figure 3.

~~~
Analyzing infrastructure --> Infrastructure.RNA
 Detecting Danger --> Safe_points.RNA
  ne14 has a Platform[plf116] @ [-1075, -450]
  ne15 has a Curve(2 lines) @ [[-710, 300]]
  ne16 has a LevelCrossing[lcr120] @ [-192, -450]
  ne18 has a Platform[plf117] @ [1111, -450]
  ne19 has a Middle point @ [347.0, 300]
  ne20 has a Middle point @ [1093.5, 300]
~~~

*Console Output 2. Infraestructure analysis and CDL zones detection.*

![Figure 3](step_C_and_D_2.png "Figure 3")
*Figure 3. Infraestructure analysis and CDL zones detection: GUI Output*

In Figure 4 is possible to view that elements:

![Figure 4](step_C_and_D_graphic.png "Figure 4")
*Figure 4. Infraestructure analysis and CDL zones detection: Layout*

### E. Generate signalling

To obtain an analysis for each network element, in the program configurations (view Figure 5) select only the option what you want. Dismark all options an keep marked only what do you need. Repeat this logic step for follows steps.

![Figure 5](config_options.png "Figure 5")
*Figure 5.*

**Signals generated due to line borders(L) and buffer stops(T):**

Configuration for this step analysis.

![Figure 6](config_1.png "Figure 6")
*Figure 6.*

Signals are enumerated since 00 with a prefix letter to indicate which element generates them. BufferStops and LineBorders signals start with T and L respectively. In Figure 7 we can visualize some of the signals generated by applying algorithm 3 explained in [1] section "III. SIGNALLING GENERATION".

In red letters, automatically added signals are shown.

The RNA allocates signals close to the buffer stops:

-- Stop: *T01*

-- Departure: *T02*

The RNA allocates signals close to the line borders:

- Departure signals: *L03, L04, L05 and L06* are assigned close to every line border that belongs to a netElement whose track is longer than a configurable fixed length.

![Figure 7](Figure1.png "Figure 7")
*Figure 7.*

**Signals generated due to line borders(L),buffer stops(T) and rail joints (J):**

The signals for rail joints are named as J and a consecutive number of signal.

Configuration for this step analysis.

![Figure 8](config_2.png "Figure 8")
*Figure 8.*

The algorithm not assigns signalling at the beginning and end of each track, because **this network not have rail joints** as shown in Figure 9.

![Figure 9](Figure2.svg "Figure 9")
*Figure 9.*

**Signals generated due to line borders(L),buffer stops(T),rail joints (J), platforms(P) and level crossings(X):**

The signals for platforms are named as P and signals for level crossings are named as X. A consecutive number of signal is assigned for each type of signalling.

Configuration for this step analysis.

![Figure 10](config_3.png "Figure 10")
*Figure 10.*

Notice that RNA can be configured to avoid adding this signalling when the level crossing and the platform are close together and therefore the signalling between them is not necessary.

In Figure 11 shown the signals (in red letters, added signals are shown):

- Generated due level corrsings: *X07 and X08*.

It is necessary to introduce signals before the train reaches the level crossing as explained in Algorithm 5, explained in [1] section "III. SIGNALLING GENERATION".

- Generated due platforms: *P09, P10, P11 and P12*.

A railway platform is where the passengers wait for trains to arrive and depart. It is necessary to have a departure signal after the platform. This is implemented using Algorithm 6 explained in [1] section "III. SIGNALLING GENERATION".

![Figure 11](Figure3.png "Figure 11")
*Figure 11.*

**Signals generated due to line borders(L),buffer stops(T),rail joints (J), platforms(P),level crossings(X) and switches(S,H,C,B):**

Configuration for this step analysis.

![Figure 12](config_4.png "Figure 12")
*Figure 12.*

The signals for switches are named based on the point they want to protect: S for Starting branch, C for the Continue branch and B for the Detour branch.  However, there are other signals named with H that are not protecting explicitly any of the three points switches have.

Signals generated for (in red letters, added signals are shown):

- Sw01:*C13, B14, S18 and H19*.
- Sw02:*C17, S15 and H16*.
- Sw03:*C20, S21 and H22*.

![Figure 13](Figure4.png "Figure 13")
*Figure 13.*

### F. Simplify signalling

The signal simplification process used by RNA relies on two main principles: i) vertical inheritance, and ii) horizontal inheritance. Both principles are explained in [1] in section "IV. SIGNALLING SIMPLIFICATION".

To simplify signals, it's needed that mark the configuration option "Simplify signals".

![Figure 14](config_5.png "Figure 14")
*Figure 14.*

After generating all the signalling, a simplification should be made to keep only the appropriate signals, as shown in Figure 15:

![Figure 15](Figure5.svg "Figure 15")
*Figure 15.*

### G. Export a resulting railway layout description

Once the signalling is generated and simplified, it is necessary to establish the railway routes to create the railway interlocking table. A railway route is the simplest path between two consecutive signals in the same direction, using the same tracks.

To obtain the table of routes it's necessary to open the archive generated for this example: "Example_2_B.railml" (if the user keep the names provided by this repository) using Rail-AID software, as shown in Figure 16.

![Figure 16](import_rail_aid_1.png "Figure 16")
![Figure 16](import_rail_aid_2.png "Figure 16")
*Figure 16. Import railml file*

Once the file was opened, it will be possible to view the network and his elements, like the Figure 17.

![Figure 17](import_rail_aid_3.png "Figure 17")
*Figure 17. Example 2 network in Rail-AID*

In the menu "View" in Rail-AID, select Routes:

![Figure 18](import_rail_aid_4.png "Figure 18")
*Figure 18. View Routes*

then Rail-AID will display the table of routs for this network. It's show in Figure 19.

![Figure 19](import_rail_aid_5.png "Figure 19")
*Figure 19. Routes in Rail-AID*

#### Original table

The original example have the follow estructure, signalling and routes, that are designed for experts and follow the RailMl standard.

![alt text](2_A.png)
*Figure 20. Original Example provided by RailMl*

| Route  | Entry | Exit | Switches | Platforms | Crossings | netElements |
|  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |
| R_01 |  S07  |  S11  | Sw01_N  | - | - | ne14-ne16 |
| R_02 |  S08  |  S11  | Sw01_R  | - | - | ne15-ne16 |
| R_03 |  S09  |  S12  | Sw02_N  | - | - | ne18-ne16 |
| R_04 |  S10  |  S13  | Sw03_N  | - | - | ne20-ne19 |
| R_05 |  S10  |  S12  | Sw03_R + Sw02_R  | - | - | ne20-ne17-ne16  |

#### Generated table

The example analysed by RNA and the aproach of this work, have the follow estructure, signalling and routes, that are the result of an automatic process and also follow the RailMl standard.

![alt text](2_B.png)

| Route  | Entry | Exit | Switches | Platforms | Crossings | netElements |
|  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |
| R_01 |  P10  |  S18  | Sw01_N  | - | - | ne14-ne16 |
| R_02 |  B14  |  S18  | Sw01_R  | - | - | ne15-ne16 |
| R_03 |  P11  |  S15  | Sw02_N  | - | - | ne18-ne16 |
| R_04 |  S21  |  T01  | Sw03_N  | - | - | ne20-ne19 |
| R_05 |  S21  |  S15  | Sw03_R + Sw02_R | - | - | ne20-ne17-ne16 |

Extra routes considering bidirectional tracks:

| Route  | Entry | Exit | Switches | Platforms | Crossings | netElements |
|  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |  :---:  |
| R_06 |  S15  |  P09  | Sw01_N  | - | Lc01 | ne16-ne14 |
| R_07 |  S15  |  L04  | Sw01_R  | - | Lc01 | ne16-ne15 |
| R_08 |  S18  |  P12  | Sw02_N  | - | Lc01 | ne16-ne18 |
| R_09 |  T02  |  L06  | SW03_N  | -  | - | ne19-ne20 |
| R_10 |  S18  |  L06  | Sw02_R + Sw03_R  | - | Lc01 | ne16-ne17-ne20 |

Routes 1 to 5 are the same in both interlocking tables, but RNA considers tracks as bidirectional while the original layout has only one direction per track. Routes 6 to 10 are the opposite of routes 1 to 5. It does not affect safety, RNA always considers every possible route in the layout. What is more, departure signal are considered for line borders and buffer stops for extra protection.

## References

[1] M. N. Menendez, S. Germino, L. Díaz-Charris, and A. Lutenberg, Automatic Railway Signalling Generation for Railways Systems Described on Railway Markup Language (railML).
