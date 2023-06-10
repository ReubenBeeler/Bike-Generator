# Bike-Generator
Authors: Reuben Beeler, Audrey O'malley, Cora Constantinescu

![Thumbnail](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/ea010aad-ff79-4312-95a7-4ae29bb19bb4)


### WELCOME!
This repository is a collection of primarily 3D-model files for our UCSB Physics 13CL, 10-week project -- a bike-driven, permanent-magnet generator that can power auxiliary electronic devices (such as a mobile phone). If you are interested in building a similar project for yourself, continue onwards! This is a comprehensive set of instructions for building our project (with special notes along the way to make the journey as seamless as possible!). 

The first detail to note about this project is that there are a few crucial, pre-existing components in this design which we had to work around, namely a permanent magnet, a USB charging cable, and a [type] bike. The design of our circuitry and 3D-printed parts had to meet the specifications and sizes of each of these components, so naturally this manual is segmented into 3 chapters. (Note that such objects come in a variety of flavors, so it is likely that slight modifications need to be made to fit your exact needs).

## 1. Generator
At the heart of this project lies the generator itself, which consists of a magnet and a coil that move relative to each other. There are lots of moving parts to consider, so in order to construct a successful generator, one should know the appropriate optimizations and constraints of electromagnetic generation. To this end, it is important to understand the physical laws which govern such phenomena; below is a brief overview.

### The Physics

Permanent magnets have a permanent magnetic field. For a cylindrical magnet polarized along its cylindrical axis (like the one used in our project), a cross section of the magnet and its magnetic field looks like the following:

![cylindrical_magnet_field_lines](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/d847dcae-2f62-47c0-b2b1-07a8fd6e49c4)

If you were to spin the magnet along its cylindrical axis, the magnetic field in 3D space would be unchanged since that axis is the axis of symmetry. If, however, you were to spin the magnet on another axis, the direction and magnitude of the field at a particular point would change as a function of time. If, perchance, this changing magnetic field penetrates a conducting material or loop of wire, the conductor will experience an induced emf characterized by Faraday's Law (equation below).


![faraday's law](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/d965ffeb-f51c-444d-aed5-78e9c1d4f25a)

We see that the induced voltage (![emf](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/6ecdb1dc-2a35-4f56-85a4-5c4d269e2d51)) in the conductor is linear to the change in magnetic flux (![magnetic flux](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/41bcfaa0-aa57-4571-b8d7-55332b00086f)) with respect to time. So, a spinning magnet near a coil/solenoid induces a voltage which drives current through a circuit, thus powering some electronic device. Before we build anything, realize that there are several considerations and optimizations to be made!

### Optimizations

Before buying magnets, magnetic wire, 3D print filament, etc., it is advised that you read this section thoroughly.

#### Magnet Strength
It is natural to search for the strongest magnet (or rather the most densely strong magnet since space is an important consideration). A permanent magnet's strength is characterized by its "maximum energy product", which specifies the greatest value of volumetric magnetic-energy density on the surface of the magnet. This is a good metric for characterizing magnetic field strength because volumetric magnet-energy density is a monotonic function with respect to magnetic field strength. Specifically, it is the following:

TODO insert equation for magnetic field density

Finding the right magnet can be difficult since there are several strains of magnets on the market! To help navigate the sea of shiny metals, consider the following graph of magnet strength over recent decades from a ScienceDirect article by Mohapatra and Liu:

![magnet strength graph](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/d09b03eb-2a04-4074-b44e-3bd2333670cc)

It is clear that neodymium-iron-boron magnets win the cake with maximum energy products reaching as high as 58 mega-guass-oersted. (The abbreviation for such a neodymium magnet is naturally N58). Unfortunately, such magnets are challenging to get any hands on; the best _accessible_ magnets for DIY projects have strengths around 50 mega-guass-oersted. [Our specific magnet](https://www.amazon.com/gp/product/B07KF61YZT/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) is a cylindrical N52 magnet, which does its job (although is more expensive then essentially identical magnets from other vendors). If you buy multiple N52 magnets together, the first difficulty will be separating them. Slide them apart, don't pull, and **NEVER** bring them back together unless you know what you are doing. These magnets are hazardous!; bringing them together will likely break them in addition to your fingers. Keep them away from computers, hard drives, and electronic devics in general.

#### Magnet-Coil Orientation
The first optimization we make is maximizing the emf by orienting the magnet and coil such that the magnet or coil rotates around an axis which is perpendicular to both the cylindrical magnet's axis _and_ the axis of the solenoid. Here is a visual supplement to thwart confusion:

TODO ADD PHOTO OF MAGNET AXIS ALIGNED WITH CYLINDER AXIS, PERPENDICULAR ROTATION AXIS

TODO Explain above image

#### Magnet Shape
While cylindrical or rectangular magnets are common, they are not ideal for a generator. Recognizing that the magnet performs circular motion relative to the surrounding coil, the magnet might as well be symmetric around the axis of rotation. Since this axis is perpendicular to the axis of the coil (a circular solenoid), a spherical magnet would utilize this "rotation space" most efficiently. We accordingly recommend that future versions use spherical N52 magnets as opposed to cylindrical N52 magnets. The rest of the project assumes a cylindrical magnet because that is simply what was available at the beginning of the project.

#### Proximity of Coil
Where in the magnetic field diagram is our cylinder? The magnetic field strength in the above field diagram (for a cylindrical magnet) is characterized by the density of magnetic field lines. Maximizing magnetic flux in our generator requires enclosing the maximum amount of field lines TODO

#### Rotor and Stator
What spins and what doesn't? An electromagnetic generator simply requires a magnet to move relative to a coil. In the user's reference frame, the magnet could spin or the coil could spin (or both!). To optimize for simplicity (to avoid the difficulty of wire brushes), the coil is kept stationary relative to the bike while the permanent magnet rotates inside the coil. To maintain this rotation, we should encapsulate the magnet in some sort of contain which we can rotate inside of the cylinder. To understand what that might look like for our cylindrical magnet, observe the following 3D model of the magnet, a "magnet holder", and the cylinder around which a coil would be wrapped.

TODO image of cylinder + rotor

TODO Explain above image more

#### Angular Frequency
How fast do (should) we spin the magnet? If the magnet is spinning with some constant angular velocity, the magnetic flux would look like

TODO add equation: PHI = PHI_0 sin(OMEGA * t)

where _TODO PHI_0_ is a constant depending on the geometry of the magnet and coil. Using Faraday's Law, we find that

TODO add equation: EMF = OMEGA * PHI_0 sin(OMEGA * t)

. So, increasing angular frequency of the magnet increases the induced emf, which pushes more current across the load. This is what we desire, yet it is important to note that operating at too high frequencies increases friction between the rotating and stationary parts of the build. This implies the existence of an optimal frequency, yet the constraint of a human turning the magnet with only mild gear reduction makes this optimal frequency beyond reach; an oscillatory frequency of about 5-10Hz is sufficient as we'll see later.

#### Number of Wire Windings
Consider a solenoid with a variable number of windings. Increasing the number of windings of the solenoid quadratically increases the absolute value of magnetic flux (and its time derivative), thus increasing the absolute value of the induced emf. In general, more wrapped wire provides more electrical generation. However, realistic wires have some resistance! Having an inductor with an enormous amount of wire (relative to the impedance of the load) would be counterproductive since most of the energy would be dissipated by the inductor's resistance. So, there must be some optimal amount of wire to use in the inductor. Unfortunately, due to the complicated nature of the various dissipative forces, it is difficult to predict what exactly that optimum is.

#### Wire Size
Which size of wire should you pick for the coil? We chose a 30 AWG copper wire... TODO complete this Knowing that we use copper wire, spin the magnet with a frequency

#### Wire Insulation
TODO COIL specs -- radius, _magnetic_ wire (enameled coating rather than PVC)
Enameled wire is harder to strip --  easiest with sandpaper or scraping with scissors but alternative methods exist like chemical bath.

#### 3D-Print Filament
PLA vs. ABS? vs. TPU, threads

### Building
...

Discuss shape of magnet holder + how the magnet fits into the magnet holder (glue?)
How rotor fits into cylinder w/ bearings to stabilize rotation.

### Testing
QUICK TEST OF GENERATOR BY TESTING VOLTAGE vs. ANGULAR FREQUENCY -- show graph(s)

## 2. Circuit
Most devices powered through USB take a voltage input of 5V DC. This motivated our next goal of converting the AC output from the generator into a usable DC current. We used the circuit pictured consisting of a bridge rectifier, a capacitor, and a voltage regulator.

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
The final circuit step was to attach it to the power bank in hopes of actually charging it. We used the USB cord that charged the power bank. Cutting it open exposed two wires, a positive and negative. We hooked those up directly to the positive and negative outputs of our circuit. We were then able to directly plug the cord into the bank.

The power bank did not charge at first. Connecting it to the circuit altered the total impedance of our circuit since the bank has some intrinsic resistance. It caused our smooth DC output to become less stable and have a lower voltage. As a result, we still had to do some more minor adjustments to the value of our capacitor. After some more guess and check, we landed on the 47𝜇F mentioned above. 

## 3. Bike Interface

## Integration Testing!
