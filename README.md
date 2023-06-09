# Bike-Generator
Authors: Reuben Beeler, Audrey O'malley, Cora Constantinescu

![Thumbnail](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/ea010aad-ff79-4312-95a7-4ae29bb19bb4)


### WELCOME!
This repository is a collection of primarily 3D-model files for our UCSB Physics 13CL, 10-week project -- a bike-driven, permanent-magnet generator that can power auxiliary electronic devices (such as a mobile phone). If you are interested in building a similar project for yourself, continue onwards! This is a comprehensive set of instructions for building our project (with special notes along the way to make the journey as seamless as possible!). 

The first detail to note about this project is that there are a few crucial, pre-existing components in this design which we had to work around, namely a permanent magnet, a USB charging cable, and a [type] bike. The design of our circuitry and 3D-printed parts had to meet the specifications and sizes of each of these components, so naturally this manual is segmented into 3 chapters. (Note that such objects come in a variety of flavors, so it is likely that slight modifications need to be made to fit your exact needs).

## 1. Generator
At the heart of this project lies the generator itself, which consists of a magnet and a coil that move relative to each other. In order to construct a successful generator, one should know the appropriate optimizations and constraints of electromagnetic generation. To this end, it is important to understand the physical laws which govern electromagnetic generation; here is a brief overview.

### The Physics

Permanent magnets have a permanent magnetic field. For a cylindrical magnet polarized along its cylindrical axis (like the one used in our project), a cross section of the magnet and its magnetic field looks like the following:

![cylindrical_magnet_field_lines](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/d847dcae-2f62-47c0-b2b1-07a8fd6e49c4)

If you were to spin the magnet along its cylindrical axis, the magnetic field in 3D space would be unchanged since that axis is the axis of symmetry. If, however, you were to spin the magnet on another axis, the direction and magnitude of the field at a particular point would change as a function of time. If, perchance, this changing magnetic field penetrates a conducting material or loop of wire, the conductor will experience an induced current characterized by Faraday's Law (equation below).

![faraday's law](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/d965ffeb-f51c-444d-aed5-78e9c1d4f25a)

We see that the induced voltage (![emf](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/6ecdb1dc-2a35-4f56-85a4-5c4d269e2d51)) in the conductor is linear to the change in magnetic flux (![magnetic flux](https://github.com/ReubenBeeler/Bike-Generator/assets/45247193/41bcfaa0-aa57-4571-b8d7-55332b00086f)) with respect to time, where magnetic flux is the flux of the magnetic field through an area enclosed by a conductor. Our conductor in question is a coil, which is best approximated as an ideal solenoid. Increasing the number of windings of the solenoid quadratically increases the absolute value of magnetic flux (and its time derivative) which increases the absolute value of the induced emf. In general, more wrapped wire provides more electrical generation; this is the first optimization to consider.

More loops, more emf but also more resistance. Emf and resistance are linear with number of loops.
As many loops as possible to make resistance of load negligible so current approaches emf/R_ind.
Although we want fewer loops since more loops make it difficult to turn and voltage regulator wastes excess voltage anyway.

Our specific magnet is an N52, which is the strongest variety of neod

TODO


To avoid the difficulty of wire brushes, the coil is kept stationary relative to the bike while the permanent magnet rotates inside the coil. Keeping the magnet inside of the cylinder is important for maintaining ... Below is [_a visual compliment_](## "an image") of the described setup.

...

Describe the magnet as N52 and what N52 means, why we chose it -- some advice/info on rare earth magnets
Spherical magnet and shape of magnet
Discuss shape of magnet holder + how the magnet fits into the magnet holder (glue?)
How rotor fits into cylinder w/ bearings to stabilize rotation.
How we determined radius of cylinder (and therefore coil) and why -- magnetic field diagram.
MATH SECTION

## 2. Circuit
## 3. Bike Interface

## Integration Testing!
