# Bluetooth Messenger Display Tutorial

## What you'll need
Programs
- KiCAD - For PCB Design
- CAD software (Onshape, Fusion360, Solidworks) - For 3D-Modeling
- Arduino IDE - For Firmware

Components
- SSD1306 OLED Display
- WeMos D1 Mini
- Custom PCB
- Case/Stand (totes optional!)
  
Optional (for portability)
- Lithium Coin Battery (2pc)
- Battery Holder (2pc)

# Step 1: Design your Circuit

Open up KiCad and create a new project and name it whatever you want! In my case, I named it bluetext. 

<img width="995" height="658" alt="image" src="https://github.com/user-attachments/assets/4856be50-c635-479e-acdb-be14578b5156" />
Select schematic editor - this is where we are laying out all our components.

Before we do anything, we want to import our symbol and footprint libraries for our components. We can either make them ourselves, or find a library online and that's exactly what we're going to do for our ESP and OLED display.

[Library for the WeMos D1 Mini](https://github.com/jerome-labidurie/d1_mini_kicad)

[Symbol and Footprint Download for OLED Display](https://www.snapeda.com/parts/DM-OLED096-636/Display%20Module/view-part/)

Once you download those, we need to import them into our project. Go to preferences and select "Manage Symbol Libaries..."

<img width="623" height="202" alt="image" src="https://github.com/user-attachments/assets/47500026-2d6f-4678-9843-05cefee746e6" />

A new window should pop up and we want to hover "Project Specific Libraires" at the top. We can select the folder symbol "Add existing library to table" near the bottom and search for the files you just downloaded. They should have the file extension ".kicad_sym". You have to do this twice for the OLED and the WeMos. 

<img width="283" height="83" alt="image" src="https://github.com/user-attachments/assets/da147dd0-035a-498b-bdce-aa92f724a722" />

Your window should look something like this. I changed the nickname for the libraries to make it easier to read. After that click "Ok"!
<img width="1258" height="831" alt="image" src="https://github.com/user-attachments/assets/c71f9d29-7098-4983-aa93-f584cab0c2ef" />

Great! Now it's time to place our components! 

<img width="1919" height="1020" alt="image" src="https://github.com/user-attachments/assets/13cb4e85-758a-4462-b3eb-543a2bcce3f7" />

Press "A" to add a part and search up your components. It's easier to search up the nickname of the libraries we just imported. Left click to place it down. 

<img width="868" height="676" alt="image" src="https://github.com/user-attachments/assets/be936908-6901-4a84-83c3-2ca175e7bec0" />

Repeat with your other component. You should see something like this:

<img width="873" height="540" alt="image" src="https://github.com/user-attachments/assets/fdb37843-872f-4207-8fe6-b4b2c49b79a1" />


Now we want to finish the circuit! We want to look at both components pinout to see what connects to what. 


<img width="500" alt="image" src="https://github.com/user-attachments/assets/76063f0b-154e-486e-960e-6ac8796412ce" />

<img width="475"  alt="image" src="https://github.com/user-attachments/assets/3d4ab8ae-3375-4b30-aaf3-4bc92487124c" />


SCL and SDA are special pins that need to be on a specific pin on our board in order to communicate properly. This is why we need to look at both pinouts to insure that we have the right connections. 

By looking at both pinouts, the following table this should be our connections.

|OLED|WeMos|
|---|------|
|VCC_IN|5V|
|SCL|D2|
|SDA|D1|
|GND|GND|

We can either wire them up manually by pressing "W" and dragging lines to each connection like this:

<img width="994" height="542" alt="image" src="https://github.com/user-attachments/assets/851942ac-82bf-43cb-a1ee-a5dabb5682a1" />

*Note: the highlighted line is crossing the SDA and SCL connection to the GND pin. It does interfer with those wires, however we might want to keep it in mind in the future.*

Or, use global tags (ctrl + L) to make our connections look cleaner. Global tags with the same name will be connected like this:

<img width="1081" height="633" alt="image" src="https://github.com/user-attachments/assets/89b30e4e-1205-489e-b25d-c5be1f4bda35" />


Either way is good and it's up to you!

Good job, we finished the schematic!

# Step 2: Design the PCB

Before we switch to our PCB editor, we have to assign footprints! Since we already downloaded the footprints, we just have to import them into our project.

In the top right toolbar select "assign footprints".

<img width="336" height="121" alt="image" src="https://github.com/user-attachments/assets/e2c71bf5-826b-4b89-8478-cf0eb81fb521" />

You should be on this window now! 

<img width="1919" height="985" alt="image" src="https://github.com/user-attachments/assets/a762f55c-84fd-49a0-be20-a148b7523bb7" />

Naviagate to preferences and go to "Manage footprint libaries". We're going to do exactly what we did before by going to "Project specific libaries" and adding an already existing folder.

It should look like this!
<img width="1264" height="833" alt="image" src="https://github.com/user-attachments/assets/4c7d9fbb-cbac-46e3-802c-e036fea801f6" />

*The file you will be downloading will be .KiCad_MOD file. However, you must select the folder that contains the file, not the file itself because it will not show up.*

To assign footprints, select a row in the "Symbol: Footprint assignments" column and search your library on the right side. It should pop up on the left column and double-click to assign. Repeat with your other part.
<img width="1112" height="129" alt="image" src="https://github.com/user-attachments/assets/6bd62d21-98d1-44fe-859d-73bb86a56325" />

Let's save and then switch the other PCB editor, at the top you can "Update PCB from Schematc" and click to place down your parts.
<img width="997" height="707" alt="image" src="https://github.com/user-attachments/assets/c7456c55-6989-4d6d-a308-feca3b29d035" />

Now this is where you get creative! Use "r" to rotate and "f" to flip your parts in whatever way you like. Afterwards, switch your layer to "Edge.Cuts" and create the shape of your board. I highly encourage you to mess around with some of the tools to see what shapes you can make! This is what mine looks like and my WeMos is flipped to the back.

<img width="1059" height="663" alt="image" src="https://github.com/user-attachments/assets/8ce9db4b-4326-486e-875c-d436901986d1" />

Now let's route our connections by pressing "w" and follow the blue rat lines by clicking a connection. Follow it to the next whole a repeat for your next 3 connections. Mine isn't the prettiest, but it will get the job done!

<img width="777" height="553" alt="image" src="https://github.com/user-attachments/assets/56413cc5-00df-4ca5-90e5-412a9c040a98" />

This is perfectly fine but I want to personalize mine a bit more. I added my name, a couple of graphics to make it my project!

<img width="962" height="615" alt="image" src="https://github.com/user-attachments/assets/20396e15-9d27-487d-85bb-e895692b76bd" />
<img width="706" height="538" alt="image" src="https://github.com/user-attachments/assets/418fbc5f-d68a-43b4-b247-b68ed7148b32" />

Ta-da! You're PCB is done!

# Step 3: Firmware
At this stage, you have creative freedom for whatever you want - make cool shapes appear, tell a short story, or communicate with the screen with Wifi or Bluetooth - (and I'm going to use Bluetooth)

Install Arduino IDE and go to Tools > Board > Boards Manager and search up esp32. Our WeMos board uses that chip and we'll find our exact model under here. Once installed, go back to Board > esp32 > WEMOS D1 MINI ESP32. This is our board! 

# Step 4: Designing your case (Optional)
