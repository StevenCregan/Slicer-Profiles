# Slicer Profiles
Slicer settings for the Motion System &amp; ToolChanger.

#### Updated Notes

By utilizing the "Custom G-Code" sections of Simplify3D and PrusaSlicer, it's possible to increase and fine-tune the actions of the toolchanger.  
Personally, I prefer to make calls to the prime and purge scripts via these custom toolchanges, as opposed to within the toolchangers tpre0.g/tpost0.g/tfree0.g files  
Please note, that the PrusaSlicer profile should be using in conjunction with https://github.com/StevenCregan/RepRapFirmware-SD/tree/working_configuration  
If you try to use it in the stock configuration, you're likely to break something.  
Please take care when using any "untested" profiles/configurations


#### Original Notes

Tool changes are actioned simply by issuing T0, T1, T2, T3 and T-1. All tool changes are firmware controlled and no tool-change scripts are required in the slicer. To unload any tool at the end of a print issue a T-1 command and the active tool will be replaced back onto it's dock.

In your start script I recommend adding the command G29 S1 to enable mesh compensation, similarly add the command G29 S2 to your ending script to disable mesh compensation. it is also important to ensure that a T command is issued at the start of the print so the ToolChanger knows which tool it is to be printing with. S3D automatically adds the relevant T command at the start of a print.

Below is an example Ending Script.

    ;Drop Bed
    G91
    G1 Z2 F1000
    G90

    ; Drop off the tool
    T-1

    ; Disable Mesh Compensation.
    G29 S2

    ; Park
    G1 X-30 Y200 F50000

    ;turn off all heaters
    M0	
