# Bike-Generator
Authors: Reuben Beeler, Audrey O'Malley, Cora Constantinescu

![Thumbnail](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/ea010aad-ff79-4312-95a7-4ae29bb19bb4)


### WELCOME!
This repository is a collection of primarily 3D-model files for our UCSB Physics 13CL, 10-week project -- a bike-driven, permanent-magnet generator that can power auxiliary electronic devices (such as a mobile phone). If you are interested in building a similar project for yourself, continue onwards! This is a comprehensive set of instructions for building our project (with special notes along the way to make the journey as seamless as possible!). 

The first detail to note about this project is that there are a few crucial, pre-existing components in this design which we had to work around, namely a permanent magnet, a USB charging cable, and a [type] bike. The design of our circuitry and 3D-printed parts had to meet the specifications and sizes of each of these components, so naturally this manual is segmented into 3 chapters. (Note that such objects come in a variety of flavors, so it is likely that slight modifications need to be made to fit your exact needs).

### Materials and Budget

| Item  | Link |
| ------------- | ------------- |
| Deep Groove Ball Bearings  | https://www.amazon.com/TIMKEN-15x35x11mm-Pre-Lubricated-Performance-Effective/dp/B08DR617F2/ref=sxts_b2b_ccp_search_w_op?content-id=amzn1.sym.5b4ffd46-5d67-49f6-8205-cc9b687c425b%3Aamzn1.sym.5b4ffd46-5d67-49f6-8205-cc9b687c425b&crid=2OAAC1KW40ZWV&cv_ct_cx=deep+groove+ball+bearing&keywords=deep+groove+ball+bearing&pd_rd_i=B08DR617F2&pd_rd_r=f78fcb4a-7ffa-4a6f-9c07-403da8807c19&pd_rd_w=qo7mz&pd_rd_wg=L0UJq&pf_rd_p=5b4ffd46-5d67-49f6-8205-cc9b687c425b&pf_rd_r=RPSWP7MGHK4HNJ28FX7F&qid=1681261523&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sprefix=deep+groove+ball+bearin%2Caps%2C163&sr=1-1-d27bdacb-ad14-3372-97fb-5f5070035007  |
| Content Cell  | Content Cell  |

## 1. Generator
At the heart of this project lies the generator itself, which consists of a magnet and a coil that move relative to each other. There are lots of moving parts to consider, so in order to construct a successful generator, one should know the appropriate optimizations and constraints of electromagnetic generation. To this end, it is important to understand the physical laws which govern such phenomena; below is a brief overview.

### The Physics

Permanent magnets have a permanent magnetic field. For a cylindrical magnet polarized along its cylindrical axis (like the one used in our project), a cross section of the magnet and its magnetic field looks like the following:

![cylindrical_magnet_field_lines](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/d847dcae-2f62-47c0-b2b1-07a8fd6e49c4)

If you were to spin the magnet along its cylindrical axis, the magnetic field in 3D space would be unchanged since that axis is the axis of symmetry. If, however, you were to spin the magnet on another axis, the direction and magnitude of the field at a particular point would change as a function of time. If, perchance, this changing magnetic field penetrates a conducting material or loop of wire, the conductor will experience an induced emf characterized by Faraday's Law (equation below).


![faraday's law](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/d965ffeb-f51c-444d-aed5-78e9c1d4f25a)

We see that the induced voltage ($\mathcal{E}$) in the conductor is linear to the change in magnetic flux ($\Phi$) with respect to time. So, a spinning magnet near a coil/solenoid induces a voltage which drives current through a circuit, thus powering some electronic device. Note that for a magnet spinning inside a single solenoid, the induced current is _alternating_ current.

### Optimizations

Before building or buying anything (magnets, magnetic wire, 3D print filament, etc.), realize that there are several considerations and optimizations to be made!

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
While cylindrical or rectangular magnets are common, they are not ideal for a generator. Recognizing that the magnet performs circular motion relative to the surrounding coil, the magnet might as well be symmetric around the axis of rotation. Since this axis is perpendicular to the axis of the coil (a circular solenoid), a spherical magnet would utilize this "rotation space" most efficiently. We accordingly recommend that future versions use spherical N52 magnets as opposed to cylindrical N52 magnets. The rest of the project assumes a cylindrical magnet because that is simply what was available at the beginning of our project.

#### Proximity of Coil
Where in the magnetic field diagram is our cylinder?... Maximizing magnetic flux (and emf, current, etc.) in our generator is achieved by maximizing the enclosed field lines per loop of wire in the coil. For a single loop of wire whose axis of symmetry would appear vertically in the field diagram, it is visually evident that the loop should be placed immediately around the cylinder to enclose the maximum number of field lines. While it is interesting to consider the optimial radius for a loop of wire with some offset along the magnet's axis, the coil will not be sufficiently large to justify further exploration of this topic; the optimal location of the coil given our needs is as close to the magnet as possible.

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
Which size of wire should you pick for the coil?... We use copper wire as it is a good, cheap conductor. Knowing the resistivity of copper wire and the expected impedance of the load (about $5\\,\text{k}\Omega$), we calculated an optimal wire gauge of about 35 AWG. This calculation maximized inductance of the solenoid over resistance of our circuit while keeping constant the volume of space filled by the wire of the solenoid (since magnetic field drops off quickly). This was a crude sort of calculation but was enough to support an argument for a very thin wire... so thin that the 35 AWG wire is difficult to handle without breaking, so we resorted to using a [CMS Magnetics 30 AWG wire](https://www.amazon.com/gp/product/B07XPS2MSM/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&th=1) for the solenoid.

**After completing the project:** In hindsight, a thicker wire (around 25 AWG) would have been a better choice for allowing more current without overheating and over-resisting; our magnetic wire was rated for $0.2\\,\text{A}$, which was easily exceeded. With the voltage regulation of $5\\,\text{V}$ for USB charging, the output power was limited to the order of a watt. Definitely experi

#### Wire Insulation
Typically, wires are insulated using a flexible variant of PVC
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
The final circuit step was to attach it to the power bank in hopes of actually charging it. We used the USB cord that charged the power bank. Cutting it open exposed two wires, a positive and negative. We hooked those up directly to the positive and negative outputs of our circuit. We were then able to directly plug the cord into the bank.

The power bank did not charge at first. Connecting it to the circuit altered the total impedance of our circuit since the bank has some intrinsic resistance. It caused our smooth DC output to become less stable and have a lower voltage. As a result, we still had to do some more minor adjustments to the value of our capacitor. After some more guess and check, we landed on the 47𝜇F mentioned above. 

## 3. Bike Interface

## Integration Testing!
Now that our generator is attached to the bike, we should be able to pedal the bike to output electricity. Before implementing the circuit, we get an AC generator output:

![AC](https://github.com/ReubenBeeler/Bike-Generator/assets/134644741/576e5a5b-3671-409f-8542-e72fc0257e8f)

In the plot we can clearly see that the voltage is zero before we start pedaling. Once the pedaling begins, the AC voltage output that we see above is produced. Now, we can add in our circuit to get a 5V DC output:

![DC](https://github.com/ReubenBeeler/Bike-Generator/assets/134644741/59ba4717-8bf9-436d-9b07-f1b292506cc5)

Using a multimeter, we measured the current flowing out of this circuit was 0.45A. Using the power relation P = IV,  we have a final power of 2.25 W supplied to the power bank. 
Now that we finally have all of the elements connected and working as expected, we can ride the bike and charge the power bank. On our power bank, the lights blinking indicates that it is charging.

INSERT VID HERE


To achieve this constant charging, we needed to pedal at a constant speed. We had to pedal somewhat quickly (about 100 rpm) but not impossibly fast, as shown in the video. 
