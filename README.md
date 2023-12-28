View this README in light-mode for best results.

# Bike-Generator
Authors: Reuben Beeler, Audrey O'Malley, Cora Constantinescu

![Thumbnail](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/ea010aad-ff79-4312-95a7-4ae29bb19bb4)


### WELCOME!
This repository is a collection of 3D-model files for our UCSB Physics 13CL, 10-week project -- a bike-driven, permanent-magnet generator that can power auxiliary electronic devices (such as a mobile phone). The final product was a stationary bike where the back wheel of a mobile bike was replaced with our mechanical generator, which was securely attached to the gears and frame of the bike. If you are interested in building a similar project for yourself, continue onwards! This is a comprehensive set of instructions for building our project (with special notes along the way to make the journey as seamless as possible!). 

The first detail to note about this project is that there are a few crucial, pre-existing components in this design which we had to work around, namely a permanent magnet, a USB charging cable, and a bike with a $135\\,\text{mm}$ rear frame/hub spacing. The design of our circuitry and 3D-printed parts had to meet the specifications and sizes of each of these components, so naturally this manual is segmented into 3 chapters. (Note that such objects come in a variety of flavors, so it is likely that slight modifications need to be made to fit your exact needs). Before we dive in, here is a brief overview of the required materials.

### Materials and Budget
The cost of the entire project, for those who already own a bike, is around $200. Do note that the below table indexes the costs of each component, even though not all materials will be fully used. For example, PLA filament typically comes in batches of a kilogram, yet the project only demands a couple hundred grams (if all parts are printed successfully).

| Item | Price |
| -------------------------- | -------------------------- |
| [30 AWG Magnetic Wire](https://www.amazon.com/TEMCo-AWG-Copper-Magnet-Wire/dp/B00IAZYI3M)  | $36.36 |
| [Indoor Bike Stand](https://www.amazon.com/SONGMICS-Indoor-Trainer-Reduces-USBT01B/dp/B07YJLTQRD/ref=sr_1_4?crid=3Q8VMSY8JQ2O5&keywords=turn+bike+into+stationary+bike&qid=1681260447&sprefix=turn+bike+%2Caps%2C177&sr=8-4)  | $59.99 |
| [Bike Sprocket](https://www.amazon.com/EBIKELING-7-Speed-Bicycle-Freewheel-Cassette/dp/B07C86GR9W/ref=sr_1_1_sspa?crid=1X0FJKQU88P97&keywords=bicycle+gears&qid=1681264320&sprefix=bicycle+gears+%2Caps%2C350&sr=8-1-spons&psc=1&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUE5MUc0NzlHMFRSNUkmZW5jcnlwdGVkSWQ9QTA4NzgzMTMxT00ySk83VUk0TTlLJmVuY3J5cHRlZEFkSWQ9QTA1MTE5MTgyOERRT0UySk9ROUFUJndpZGdldE5hbWU9c3BfYXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ==)  | $18.98 |
| 2 608Z Ball Bearings | $10 |
| [Bridge Rectifier](https://www.amazon.com/Bridgold-KBPC5010-Rectifier-Electronic-Silicon/dp/B07MQ65HLB/ref=sr_1_3?crid=RE6GX8ZWP371&keywords=bridge+rectifier&qid=1686367944&sprefix=bridge+re%2Caps%2C165&sr=8-3) | $8.99 |
| [Jumper Wire Kit](https://www.amazon.com/dp/B07CJYSL2T?psc=1&ref=ppx_yo2ov_dt_b_product_details)| $11.99 |
| [5V Voltage Regulator](https://www.amazon.com/dp/B07T5ZHY63?psc=1&ref=ppx_yo2ov_dt_b_product_details)| $13.99 |
| [Heat Sink](https://www.amazon.com/dp/B07ZMH4FDW?psc=1&ref=ppx_yo2ov_dt_b_product_details) | $6.99 |
|[Magnet](https://www.amazon.com/gp/product/B07KF61YZT/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)| $16.99 |
|3D Printer Filament| $20.00 |
|Galvanized Hex Bolt: 3/8 inch diameter, 1 inch long| $2 |
|Galvanized Hex Bolt: 3/8 inch diameter, 2.5 inch long| $2 |
|2 Galvanized Hex Nuts: 3/8 inch diameter| $2 |
|Bicycle| -- |
|Desired USB Powered Electronic Device| -- |


## 1. Generator
At the heart of this project lies the generator itself, which consists of a magnet and a coil that move relative to each other. There are lots of moving parts to consider, so in order to construct a successful generator, one should know the appropriate optimizations and constraints of electromagnetic generation. To this end, it is important to understand the physical laws which govern such phenomena; below is a brief overview.

### The Physics

Permanent magnets have a permanent magnetic field. For a cylindrical magnet polarized along its cylindrical axis (like the one used in our project), a cross section of the magnet and its magnetic field looks like the following:

![cylindrical_magnet_field_lines](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/d847dcae-2f62-47c0-b2b1-07a8fd6e49c4)

If you were to spin the magnet along its cylindrical axis, the magnetic field in 3D space would be unchanged since that axis is the axis of symmetry. If, however, you were to spin the magnet on another axis, the direction and magnitude of the field at a particular point would change as a function of time. If, perchance, this changing magnetic field penetrates a conducting material or loop of wire, the conductor will experience an induced emf characterized by Faraday's Law (equation below).


![Faraday's law](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/f2302e99-7201-4eea-bf75-18e710c6815b)

We see that the induced voltage ($\mathcal{E}$) in the conductor is linear to the change in magnetic flux ($\Phi$) with respect to time. So, a spinning magnet near a coil/solenoid induces a voltage which drives current through a circuit, thus powering some electronic device. Note that for a magnet spinning inside a single solenoid, the induced current is _alternating_ current.

### Optimizations

Before building or buying anything (magnets, magnetic wire, 3D print filament, etc.), realize that there are several considerations and optimizations to be made!

#### Magnet Strength
It is natural to search for the strongest magnet (or rather the most densely strong magnet since space is an important consideration). A permanent magnet's strength is characterized by its "maximum energy product", which specifies the greatest value of volumetric magnetic-energy density on the surface of the magnet. This is a good metric for characterizing magnetic field strength because volumetric magnet-energy density is a monotonic function with respect to magnetic field strength. Specifically, it is the following:

![magnetic energy density](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/2d41e40c-8120-4198-8527-2ba5b72bda8a)

Finding the right magnet can be difficult since there are several strains of magnets on the market! To help navigate the sea of shiny metals, consider the following graph of magnet strength over recent decades from a ScienceDirect article by Mohapatra and Liu:

![magnet strength graph](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/d09b03eb-2a04-4074-b44e-3bd2333670cc)

It is clear that neodymium-iron-boron magnets win the cake with maximum energy products reaching as high as 58 mega-guass-oersted. (The abbreviation for such a neodymium magnet is naturally N58). Unfortunately, such magnets are challenging to get any hands on; the best _accessible_ magnets for DIY projects have strengths around 50 mega-guass-oersted. [Our specific magnet](https://www.amazon.com/gp/product/B07KF61YZT/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) is a cylindrical N52 magnet, which does its job (although is more expensive then essentially identical magnets from other vendors). If you buy multiple N52 magnets together, the first difficulty will be separating them. Slide them apart, don't pull, and **NEVER** bring them back together unless you know what you are doing. These magnets are hazardous!; bringing them together will likely break them in addition to your fingers. Keep them away from computers, hard drives, and electronic devics in general.

#### Magnet-Coil Orientation
The first optimization we make is maximizing the emf (change in magnetic flux) by orienting the magnet and coil such that the axis of rotation is perpendicular to both the cylindrical magnet's axis _and_ the axis of the solenoid. Here is a visual supplement to thwart confusion:

![Cylinder-Magnet Rotation Axis](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/ba30fcff-b8dc-4b26-bdd2-0c8897f67ef4)

#### Magnet Shape
While cylindrical or rectangular magnets are common, they are not ideal for a generator. Recognizing that the magnet performs circular motion relative to the surrounding coil, the magnet might as well be symmetric around the axis of rotation. Since this axis is perpendicular to the axis of the coil (a circular solenoid), a spherical magnet would utilize this "rotation space" most efficiently. We accordingly recommend that future versions use spherical N52 magnets as opposed to cylindrical N52 magnets. The rest of the project assumes a cylindrical magnet because that is simply what was available at the beginning of our project.

#### Proximity of Coil
Where in the magnetic field diagram is our cylinder?... Maximizing magnetic flux (and emf, current, etc.) in our generator is achieved by maximizing the enclosed field lines per loop of wire in the coil. For a single loop of wire whose axis of symmetry would appear vertically in the field diagram, it is visually evident that the loop should be placed immediately around the cylinder to enclose the maximum number of field lines. While it is interesting to consider the optimial radius for a loop of wire with some offset along the magnet's axis, the coil will not be sufficiently large to justify further exploration of this topic; the optimal location of the coil given our needs is as close to the magnet as possible.

#### Rotor and Stator
What spins and what doesn't? An electromagnetic generator simply requires a magnet to move relative to a coil (which is wrapped around a hollow cylinder). In the user's reference frame, the magnet could spin or the coil could spin (or both!). To optimize for simplicity (to avoid the difficulty of wire brushes), the coil and cylinder (called the "stator") are kept stationary relative to the bike while the permanent magnet and "magnet holder" (called the "rotor") rotate inside the coil. To help understand what that might look like for our cylindrical magnet, the standalone rotor (magnet and magnet holder) looks like this:

![Rotor](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/4e0d0b35-5494-42e8-a051-dbd0821c4e6d)

The rotor combined with the cylinder looks like this:

![Cylinder Right smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/c5b4dd40-78a1-46f1-a837-df1e51105b65)
![Cylinder Front Right smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/1c116fbc-ac2c-4706-ab21-489a8e2f647f)

#### Angular Frequency
How fast do (should) we spin the magnet? If the magnet is spinning with some constant angular velocity, the magnetic flux would look like

![phi equation](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/617fcc58-9d9d-4b6c-b9eb-b071cd0e5b8d)

where $\Phi_0$ is a constant depending on the geometry of the magnet and coil. Using Faraday's Law, we find that

![emf as function of omega](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/4bc19276-617b-4ed0-a1dd-e7697ee37089)

So, increasing angular frequency of the magnet increases the induced emf, which pushes more current across the load. This is what we desire, yet it is important to note that operating at too high frequencies increases friction between the rotating and stationary parts of the build. This implies the existence of an optimal frequency, yet the constraint of a human turning the magnet with only mild gear reduction makes this optimal frequency beyond reach; an oscillatory frequency of about 5-10Hz is sufficient as we'll see later.

#### Number of Wire Windings
Consider a solenoid with a variable number of windings. Increasing the number of windings of the solenoid quadratically increases the absolute value of magnetic flux (and its time derivative), thus increasing the absolute value of the induced emf. In general, more wrapped wire provides more electrical generation. However, realistic wires have some resistance! Having an inductor with an enormous amount of wire (relative to the impedance of the load) would be counterproductive since most of the energy would be dissipated by the inductor's resistance. So, there must be some optimal amount of wire to use in the inductor. Unfortunately, due to the complicated nature of the various dissipative forces, it is difficult to predict what exactly that optimum is.

#### Wire Size
Which size of wire should you pick for the coil?... We use copper wire as it's a good, cheap conductor. Knowing the resistivity of copper wire and the expected impedance of the load (about $5\\,\text{k}\Omega$), we calculated an optimal wire gauge of about 35 AWG. This calculation maximized inductance of the solenoid over resistance of our circuit while keeping constant the volume of space filled by the wire of the solenoid (since magnetic field drops off quickly). This was a crude sort of calculation but was enough to support an argument for a very thin wire... so thin that the 35 AWG wire is difficult to handle without breaking, so we resorted to using a [CMS Magnetics 30 AWG wire](https://www.amazon.com/gp/product/B07XPS2MSM/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&th=1) for the solenoid.

**Post-project note:** In hindsight, a thicker wire (around 25 AWG) would have been a better choice for allowing more current without overheating the wire: our magnetic wire was rated for $0.2\\,\text{A}$, which was easily exceeded. With the voltage regulation of $5\\,\text{V}$ for USB charging, the output power was limited to the order of a watt. For a more powerful USB charger (our end goal), we advise using a thicker wire.

#### Wire Insulation
Typically, wires are insulated using a flexible variant of PVC. This is great for increasing durability of dangling wires, however it is very space-inefficient for constructing a solenoid. The common solution for such a problem is buying wire with an enamel coating, called _magnetic_ wire. This enamel coating has a darkish-orange color similar to copper and is notoriously difficult to strip. Typical wire strippers are generally incompetent for removing enamel coating (especially on very small wires such as 30 AWG), so the next best methods are a) scraping with a knife or scissors and b) using sandpaper of roughly P200 grit.

#### 3D-Print Filament
This project involves a decent amount of 3D printing, and printing the provided STL files with the wrong settings can easily break a build. Choosing the correct settings comes with experience, but choosing the correct materials can be done from the get-go. The filament used in our final project was PLA, a 3D-printing standard which worked sufficiently well. Some problems introduced themselves when printing the magnet holder, which has threads of diameter $8\\,\text{mm}$ and pitch $1.25$. Printing the rotor horizontally flat, even with layer height of $0.05\\,\text{mm}$$, leads to enough imprecision when printing the threads that a nut cannot be screwed on (a problem which becomes evident later). Printing the rotor vertically fixes the layer-height imprecision issue, but causes the rotor to be weaker under torsion. This allows the rotor to break easily when given a strong rotation acceleration. In the end, the rotor was printed horizontally with increased shell count to solve the torsion issue, while we used a tap set to fix the imprecise threading issue.  During your 3D-printing, ensure that the layer height is $0.05\\,\text{mm}$ when printing the threads. Additionally, the rotor (and any other parts which experience significant stress) should be printed with about 80% infill to prevent breaking.

We did experiment with TPU, as it is a flexible and more durable alternative to PLA, but thread precision and tapping is an issue; it is a notable candidate worth trying, but PLA does the job.

### Building
Given the above information, the design of the generator follows accordingly. The magnet holder slides through a slit in the cylinder, after which the magnet may be inserted. The magnet holder, as depicted above in the Rotor and Stator section, fits around our magnet snugly without the need of an adhesive. In order to stabilize the rotation of the rotor, we use two 608Z ball bearings ($8\\,\text{mm}$ inner radius, $22\\,\text{mm}$ outer radius, $7\\,\text{mm}$ height), one on each side of the rotor. The outside of the bearings are stationary with the cylinder and fit snugly into the two circular slots, while the inside of the bearing rotates with the rotor. The bearings (depicted as gray disks) are visualized below: top view is on left, bottom view is on right.

![Bearing and Nut 1](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/3e55df0b-5ab6-4e29-ba10-633db7210ccd)
![Bearing and Nut 2](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/7e76430d-a839-4b13-a214-37f87c0af9e4)

In the above pictures, two 3D-printed nuts (in black) keep the rotor in the correct vertical alignment. Without such nuts, the magnet is attracted to one bearing or the other, pulling the rotor far enough to one side that it collides with the inside of the cylinder.

The next obvious step is to create the coil, which should be wrapped as close to the center as possible for reasons discussed earlier. Our generator functioned with just 300 turns; the exact number depends on your needs.

Finally, we should test the generator, which requires a method of rotating the rotor. A simple hand-crank is a practical solution for testing and debugging. The provided hand-crank in this repository is essentially an extension of a nut which screws onto the longer threaded side of the rotor as seen below.

![Cylinder Hand Crank Interface](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/ae20f559-c551-48b9-bfd4-ba9fdf50f4d7)

### Testing
In order to test that our generator was working properly, we used both a fan motor and a hand crank to drive the rotor. An oscilloscope trace of the output is below.

![ac scope trace](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/482bb655-9bef-440c-b48f-3c9cb9f51506)

Then, we tested the voltage amplitudes at different frequencies and compiled their results to produce the the following plot.

<img width="400" alt="Voltage vs Frequency" src="https://github.com/ReubenBeeler/Bike-Generator/assets/110072246/680f13eb-de3f-478e-b0af-822359e30014">

Here we see a linear relationship between frequency and voltage maximum. This is confirmed by theory and gives us the following value of $\Phi_{0}$.

<img src="https://github.com/ReubenBeeler/Bike-Generator/assets/110072246/e1f1a36b-66e6-429a-8de4-5e3054996da1" height="100">


## 2. Circuit
Most devices powered through USB take a voltage input of 5V DC. This motivated our next goal of converting the AC output from the generator into a usable DC current. We used the circuit pictured consisting of a bridge rectifier, a capacitor, and a voltage regulator. We used an oscilloscope to collect all of the following scope traces.

![circuit diagram](https://github.com/ReubenBeeler/Bike-Generator/assets/134644741/14eb47b8-220e-4459-ad16-2f7ab0d1c105)

### Full Bridge Rectification
The first part of our circuit is a bridge rectifier which is a set of four diodes arranged such that during the positive half of the voltage period, the current flows through one pair of diagonal diodes, and through the other pair on the negative half of the period. This resulted in a full bridge rectification where the output was an entirely non-negative voltage. This is exemplified by this transition from an AC voltage on the left ranging from -8V to 8V to an oscillating DC voltage on the right ranging from 0V to 8V. The frequency also nearly doubles after rectification since all of the AC troughs were rectified to become positive peaks. 

![full bridge rectification](https://github.com/ReubenBeeler/Bike-Generator/assets/134644741/99cf739e-5432-422d-ad27-4cd0bac6ac53)

### Capacitor Smoothing
The next component of our circuit is a smoothing capacitor with a capacitance of 47𝜇F. This capacitor acts as a buffer by charging up as the voltage input increases. Then, as the rectifier voltage falls, the capacitor provides the required voltage to keep the overall voltage output steady. This leaves us with a DC voltage. This is demonstrated in the plots below; on the left, the rectified voltage ranging from 0V to 8V is transformed into a constant 7V DC after the capacitor, shown on the right.

![capacitor smoothing](https://github.com/ReubenBeeler/Bike-Generator/assets/134644741/2d92b6fd-0c30-45af-afc6-7f4e5a5e221b)

At this step, we had to try many different circuit components and arrangements before we achieved this consistent DC voltage; i.e. different capacitor values, adding resistors, and moving them to different locations and orientations in the circuit. It depended on the voltage and frequency we were inputting into the circuit. The most effective method for us was trial and error, so for more drastically different inputs, there may need to be slight alteration to the circuit. 

### Voltage Regulation
The last component of our circuit was a voltage regulator which will generate a fixed output voltage. We chose a L7805 voltage regulator which caps the voltage at 5V– exactly what a USB powered electronic device expects. The voltage regulator works by dissipating the excess power in heat meaning we need to attach a heat sink to it to prevent it from overheating. In the plots below we can see that the voltage regulator transformed the 7V DC input on the left to a 5V DC output on the right. It also smoothed out any small oscillations or noise that can be seen in the input voltage on the left.

![voltage regulation](https://github.com/ReubenBeeler/Bike-Generator/assets/134644741/d21bb65b-7dc0-443f-bc8f-4355500eabef)

It is important to also note that every voltage regulator will have a dropout voltage. This is the minimum value of the difference between the input voltage and the output voltage for it to function correctly. A 5V voltage regulator has a dropout voltage of 2V meaning that it needs a minimum input of 7V. If less than 7V is provided, regulation will not occur. However, a voltage that is too high can also cause complications. A 5V voltage regulator has a maximum input of 35V. If the input voltage gets too high, you risk damaging the component. 

### Connection to the Power Bank
The final circuit step was to attach it to the power bank in hopes of actually charging it. We used the USB cord that charged the power bank. Cutting it open exposed two wires, a positive and negative (since it is a no-media cable). We hooked those up directly to the positive and negative outputs of our circuit. We were then able to directly plug the cord into the bank.

The power bank did not charge at first. Connecting it to the circuit altered the total impedance of our circuit since the bank has some intrinsic resistance. It caused our smooth DC output to become less stable and have a lower voltage. As a result, we still had to do some more minor adjustments to the value of our capacitor. After some more guess and check, we landed on the 47𝜇F mentioned above. 

## 3. Bike Interface
Recall the main goal of the project... generating power with a _bike_. Attaching the generator to the bike requires some interface between each end of the generator and the bike frame. The side of the bike with the chain should have a set of gears which connects directly to the rotor, forming the rotating interface. The other side of the frame simply connects to the cylinder, both of which are stationary, hence forming the stationary interface. These two interfaces together complete the bike interface.

### Rotating Interface
The gears (which have built-in ball bearings) should rest on a stationary 2.5-inch long, galvanized hex bolt. This bolt will be fastened to the chain-side of the bike using a galvanized hex nut. However, the bolt doesn't just magically fit into the gears; the design for the gear interface with the bolt consists of two 3D-printed parts (shown below). The left piece fits snugly around the head of the bolt, while the right one fits somewhat loosely on top of the gear. A tight fit for the latter piece is not needed as it will be kept in place from lateral pressure when placed on the bike. It also serves as a spacer between the frame and gears; feel free to adjust its width to match the hub and gear spacing on your particular bike.

![bolt smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/dadb477e-90a0-47e7-a813-bb0053980214)
![gear smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/35f8442c-ad3d-4bd0-bc96-7f62a41e9386)

Putting the bolt and gears together, it should look something like this:

![gear face smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/9c045875-7bde-4639-8869-e92a159bedb9)
![gear and bolt smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/0b87a1fb-f378-45c6-83e3-48f60d0a2347)

Once that is done, the gear will need to interface with the rotor. Conveniently, there is a set of 6 regular hole patterns in the gears. We capitalize on this by creating an attachment to the rotor (similar to the hand-crank), which we call "gear fingers". The gear fingers have 6 protrusions "fingers" which snugly fit into the 6 holes of the gears. At the center of the gear fingers lies a threaded hole which screws onto the longer side of the rotor, just next to the 3D-printed nut. The next two images show the gear fingers attached to the rotor. Note the bearing, which is just next to the threaded section of the magnet holder. Note also that the 3D-printed nut (which would be inbetween the gear fingers and the bearing) is not present in this photo. (During the process of debugging, you may find that the nuts are not necessary or that only one nut is needed).

![gears rotor 1 smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/fdf8ca22-5f37-4125-ba7a-4eee51d07286)
![gears rotor 2 smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/44c5cf1c-59ff-4378-844c-a80f1197dbd5)

Finally, ensure that the gear fingers fulfill their requirement of fitting snugly into the gears. They should look like this:

![gears fingers rotor smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/fc3280ba-e9ae-4b1c-9c77-85587d77470a)

The galvanized hex bolt from before is not shown in this photo. When attaching the generator to the bike, the gear fingers will cover the head side of the hex bolt while the tail end will attach to the bike frame.

### Stationary Interface
The stationary interface has no moving parts and is consequently a little more straightforward. The cylinder interfaces with the bike using a hex bolt & nut and a single 3D-printed part. The threaded part of the cylinder screws into this 3D-printed interface, which holds in place the 1-inch galvanized hex bolt in a fashion similar to the previous section. The 3D-printed piece appears below.

![stat-face smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/9b2c34ca-bd43-48e8-94e9-64620137bd0b)
![stat-face bolt smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/b1109cb6-d060-4bba-acca-9f6f40a2d5a2)

Here is a before-after shot of the cylinder to clarify how the result of the stationary interface should look.

![cylinder smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/d06bfbe5-07ed-4441-9a65-986cb4fae261)
![cylinder stat-face bolt smaller](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/900d82c6-ca57-4f77-9cdb-2fe10f1ce2e3)

### Integration Testing!
The entire generator with the bike attachments is finally complete!

![full generator](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/072f5a56-2d52-425a-a607-23a13a09a722)

To put the generator on the bike, simply remove the back wheel of the bike and place the bike frame onto the two protruding hex bolts. Screwing on the hex nuts should ensure a tight fit. To ride the bike, prop up the back in whatever way possible! We used an overqualified [bike stand](https://www.amazon.com/SONGMICS-Indoor-Trainer-Reduces-USBT01B/dp/B07YJLTQRD/ref=sr_1_4?crid=3Q8VMSY8JQ2O5&keywords=turn+bike+into+stationary+bike&qid=1681260447&sprefix=turn+bike+%2Caps%2C177&sr=8-4) designed for cyclist training.

The rotor should spin smoothly when turning the pedals. If the rotor wobbles, adjust the location of the hex bolts on the frame. Note that when moving the pedals sufficiently fast, the rotor may come in contact with the cylinder (if not setup properly) and melt either the rotor or the cylinder, which is pretty cool but also something to be weary of! 

Now that our generator is attached to the bike, we should be able to pedal the bike to output electricity. Before connecting the circuit, we get the following AC generator output:

<img width="400" alt="AC" src=https://github.com/ReubenBeeler/Bike-Generator/assets/134644741/576e5a5b-3671-409f-8542-e72fc0257e8f>

In the plot, we can clearly see that the voltage is zero before we start pedaling. Once the pedaling begins, the expected AC voltage output is produced. Next, we can add our circuit to obtain a 5V DC output:

<img width="400" alt="DC" src=https://github.com/ReubenBeeler/Bike-Generator/assets/134644741/59ba4717-8bf9-436d-9b07-f1b292506cc5>

Using a multimeter, we measured the current flowing out of this circuit was $0.45\\,\text{A}$. Using the power relation $P = IV$,  we have a final power of $2.25\\,\text{W}$ supplied to the power bank. Note that by adding/changing wire and making a few small modifications, this generator is capable of sustaining much more power output; for the purpose of charging our power bank, however, it turns out that $2\\,\text{W}$ is sufficient.

Now that we finally have all of the elements connected, we can ride the bike and charge the power bank as expected. The blinking lights on the power bank in the bottom-left hand corner of the below video indicate that our power bank is indeed charging.

https://github.com/ReubenBeeler/Bike-Generator/assets/110072246/ba390a81-985c-445b-9bbe-54cf46ee8960

To achieve this constant charging, we needed to pedal at a constant speed. We had to pedal somewhat quickly (about 100 rpm) but not impossibly fast, as shown in the video. 
