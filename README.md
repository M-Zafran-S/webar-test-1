-Dynamic Multi-Target WebAR Experience-
An open-source, lightweight Web-based Augmented Reality (WebAR) application built using MindAR and A-Frame. This application uses a single-page URL routing system to dynamically load unique 3D assets depending on which QR code is scanned by the user.



--📁 Repository Structure--
To ensure the application runs smoothly, always maintain the file structure exactly as organized below:
-------------------------------------------------------------------------------------------
/webar-project-root
│
├── index.html              <-- Core Router (Processes URL parameters & loads the camera)
│
├── /assets                 <-- Central Folder for App Media
│   │
│   ├── /tracking-files     <-- Place your compiled target (.mind) files here
│   │   ├── card-alpha.mind
│   │   └── card-beta.mind
│   │
│   └── /models             <-- Place your 3D assets (.glb or .gltf) here
│       ├── model-alpha.glb
│       └── model-beta.glb
│
└── README.md               <-- System Documentation & Upkeep Guide
-------------------------------------------------------------------------------------------



--🛠️ How to Add a New QR Code / 3D Target--
The client or any administrator can expand this app to support infinite pictures by following these steps:

Step 1: Compile the New Target Image
Edit your QR code at https://generatorqr.com/.

Edit the frame background color or leave it as white (#FFFFFF) and the change text to the name of target object. You can also use abbreviation if the name is too long.

Download the image, save file with same name as target object, then go to the free MindAR Online Compiler Tool at https://hiukim.github.io/mind-ar-js-doc/tools/compile/.

Upload your image, let the system process the tracking points, and download the exported file.

Rename that file (e.g., alpha.mind) and drop it into the /assets/tracking-files/ directory.

Step 2: Prepare Your 3D Asset
Ensure your new 3D asset is exported in the Binary glTF (.glb) format.

Drop the 3D asset file into the /assets/models/ directory.

Step 3: Register the Object in index.html
Open index.html in a standard text editor. Locate the arRegistry block at the top of the script tag and add a new key configuration entry following this layout:
-------------------------------------------------------------------------------------------
const arRegistry = {
  // Existing targets...
  "alpha": { ... },
  
  // ADD YOUR NEW TARGET CONFIGURATION HERE:
  "newcampaign": {
    tracking: "./assets/tracking-files/poster-new.mind",
    model: "./assets/models/model-new.glb",
    scale: "1 1 1",      // Adjust size multiplier here
    rotation: "0 0 0"    // Adjust 3D tilt/angle here
  }
};
-------------------------------------------------------------------------------------------

Step 4: Generate the Unique QR Link
Now, configure your QR code generator to print this exact web address structure:
https://yourdomain.com/?object=newcampaign

When users scan that code, the app will instantly boot up, check for the string newcampaign, and isolate your newly mapped asset configurations without disturbing the rest of the application.



--⚠️ Content Optimization Guidelines--
To keep the application highly responsive on standard cellular data grids and prevent mobile phone browsers from crashing, all digital creative teams must adhere to these structural guardrails:

Secure Hosting: The application must run on an HTTPS secure server. Mobile operating systems strictly block camera access on standard http:// links.

3D File Extensions: Only utilize consolidated .glb or binary layout configurations. Avoid .fbx or .obj data paths.

Polygon Allocations: Restrict individual 3D objects to a maximum density profile of 30,000 polygons.

Texture Maps: Cap resolutions tightly at 1024x1024 pixels maximum.

Weight Ceiling: No single 3D file asset should exceed 5MB total package weight.