Last Updated: 2024/05/27

# Stellaris-STED Confocal Microscope Instructions Manual

Python scripts for reading and converting Leica `.lif` files (`lif-reader.py` and the work-in-progress `WIP_leica_lif_processor.py`) are in the [`tools/` folder on GitHub](https://github.com/CSI-Microscopy/Stellaris-STED-Confocal/tree/main/tools).

## Starting the System

1. **Power On the Controller**:
   - Turn on the power switch on the left side.
   - Turn on the laser switch.
   - Turn the key to the "on" position.

2. **Log In to Bookit booking System**:
   - Use your credentials:
     - **Username**: Your email address.
     - **Password**: Your email address password.
   - Verify that your booking is approved. Contact a facility member if your appointment status is pending.
   - Click "Log In" and then click "Activate Service."

## Configuring the Microscope

1. **Select Configuration**:
   - After logging in, wait for the dialogue box to appear.
   - In "Configuration" choose: **Machine**.
   - In "Microscope" choose: **DMI8**.
   - Click "OK."

> [!Caution]
> Ensure the objective is set to the smallest magnification (10X) to avoid damage to the microscope.

2. **Motorized Stage Setup**:
   - When prompted about the motorized stage, click "Yes" to enable X & Y movement.

3. **Software Interface**:
   - The interface will load in about 1-2 minutes.
   - The interface is divided into widgets:
     - **Left Side Widgets**: Scan mode (Left) and Z stack (Right) settings.
    
       
       
     <img width="263" alt="2024-05-26_16h50_42" src="assets/widget-scan-mode.png">
     
     <img width="257" alt="2024-05-26_16h50_54" src="assets/widget-z-stack.png">


     - **Right Side Widgets**: Objective selection (Left), laser, and detectors settings(Right).
    
       
       
     <img width="657" alt="2024-05-26_16h50_32" src="assets/widget-objective.png">
     
     <img width="655" alt="2024-05-26_16h50_24" src="assets/widget-lasers-detectors.png">


## Setting Up for Imaging

1. **Verify Objective Magnification**:
   - Ensure the microscope is set to 10X magnification. If not, inform the staff and change it.

2. **Detector Settings**:
   - Detectors: HyD S & HyD X.
     - HyD S: Efficient for UV to yellow spectrum.
     - HYD X: Efficient for yellow to far-red spectrum.
   - Use the fluorophore panel to assign fluorophores to the appropriate detectors by dragging them from the search results.

3. **Turning On the White Light Laser (WLL)**:
   - When prompted, click "Yes" to turn on the WLL (White Light Laser).
   - Ensure no emission spectrum overlap to avoid crosstalk.

4. **Default Parameters**:
   - Lasers: 5%
   - Detectors: 10%
   - Adjust settings as needed based on your experimental requirements.

5. **Image Acquisition Settings**:
   - Avoid taking too many or too few pixels to ensure manageable image sizes and useful resolution for analysis.
   - Your object of interest (e.g., nuclei) should be defined with 5-10 pixels in each axis; you can adjust the pixel size accordingly in the scan mode widget (by increasing pixel density or by switching to a higher mag. objective).
   - Use the "Projects" tab to properly name your files, including dates, magnification, and fluorophores used.
   
> [!TIP]
> Name your project as YYYY-MM-DD-your-project-name.
> In case you acquired multiple images `(nImages>10)`, it is recommended to split the `.lif` project to multiple `.lif` files
> that contain up to 15 images. In case of missing data, you don't lose an entire dataset.
> You can start naming your images while acquiring them. It is a good way to avoid confusion at the end of the session.

> [!IMPORTANT]
> Save images to the image analysis server: `Z:/projects/your_lab_folder`

## Shutting Down the System

1. **Save and Close Files**:
   - Save all your files.
   - Right-click on the project line and select "Close All."
   - Reset acquisition parameters to default.
   - Delete detector settings by clicking the "X", reset (right-click) or trash button.

2. **Clean and Remove Sample**:
> [!Caution]
> Ensure the objective is set to the smallest magnification (10X) to avoid damage to the microscope.
   - Remove your sample and clean the microscope room.

3. **Close Software and Log Off**:
   - Close the software (this may take up to 2 minutes).
   - Log off from Bookit system.
> [!IMPORTANT]
> Log off only when you are sure everything is properly closed and your data is saved in your folder.

4. **Turn Off the Controller**:
   - Switch off the key.
   - Turn off the laser switch.
   - Turn off the power switch.

## Following these instructions will help ensure proper use and maintenance of the microscope, as well as facilitate smooth transitions between users.
