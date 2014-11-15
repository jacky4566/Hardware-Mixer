                          Mixology
						  
  What is it?
  -----------
  Software to control a mixer identical to Windows sndvol.
  The goal of this project is one part hardware and one part software.
  This repository is the interface between hardware and the Windows core audio interface.
  
  The Hardware
  -----------
  The purpose of the hardware device is to emulate sndvol in appearance and control. This will consist of 1 slider for each active program and 1 master volume command. 
  The hardware device in its current form exists as follows:
  5 - 10k Slide Potentiometers
  4 - 0.96in Full color OLED displays
  1 - Momentary mute switch
  1 - Arduino Uno communicating through a USB COM Port. 
  
  Arduino Communication
  -----------
  Once connected on the appropriate COM Port the Arduino will begin to broadcast the position of each slider and the mute state as such:
  
  Info: Mute State:(Return a byte with either 't' or 'f')
  Info: SliderA:(Returns and int of 0 to 1023)
  Info: SliderB:(Returns and int of 0 to 1023)
  Info: SliderC:(Returns and int of 0 to 1023)
  Info: SliderD:(Returns and int of 0 to 1023)
  
  To communicate with the Arduino the following commands have been setup.
  Flush:
  Send a new line '/n' to flush the serial buffer
  
  Mute mode:
  Send 'm' or 'M' followed by 't' or 'T' to set the mute mode to True, or 'f' or 'F' to set the mute mode to False
  
  Set level:
  Send 'l' or 'L' followed by the level monitor number (0-7) then the new level as an integer between 0 and 64.
  Example. L516 would set the 5th level monitor (R of display 3) to 64
 
  Set image:
  Image must be sent in chucks of 64x8. Displays have be interlaced to reduce buffer costs.
  Send 'i' or 'I' followed by the display number 1-4 then the image part 1-8. Then send 512 bytes of color data.
  Example. I24... will draw a new image in section 4 of monitor 2.
  
  