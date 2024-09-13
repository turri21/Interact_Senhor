-=(Senhor Notes)=-

Framework update to fix black screens

Adjustments for the new framework to work:
HPS_BUS changed from [45:0] to [48:0]

wire [15:0] joystick_analog_0, joystick_analog_1;   ->   wire [15:0] joystick_analog_l0, joystick_analog_l1;

hps_io #(.CONF_STR(CONF_STR)) hps_io
(
...
...
.joystick_l_analog_0(joystick_analog_l0), 
.joystick_l_analog_1(joystick_analog_l1),
...
...
)

All references to joystick_analog renamed to joystick_analog_l0 and l1 respectively 

5'b??010 : io_rd_rtc_ad = {~joystick_analog_l0[7], joystick_analog_l0[6:0]};

5'b??100 : io_rd_rtc_ad = joystick_1[4] ? 8'h00 : 8'h80;

5'b??101 : io_rd_rtc_ad = {~joystick_analog_l1[7], joystick_analog_l1[6:0]};


emu emu(
...
...
//.HDMI_BLACKOUT(hdmi_blackout),
//`ifndef MISTER_DUAL_SDRAM
//	.VGA_DISABLE(VGA_DISABLE),
//`endif
...
...
);

# [Interact](https://en.wikipedia.org/wiki/Interact_Home_Computer) for [MiSTer Platform](https://github.com/MiSTer-devel/Main_MiSTer/wiki)

<p align="center">
  <img width="320" height="240" src="https://user-images.githubusercontent.com/105246/129508473-bd14a5fa-3d2d-439b-a9a8-3a239660182f.gif">
</p>

FPGA recreation of the Interact Home Computer from 1978.  You can read about it on [Wikipedia](https://en.wikipedia.org/wiki/Interact_Home_Computer) and [Old-Computers.com](https://www.old-computers.com/museum/computer.asp?c=1004&st=1).  Core created by [@edanuff](https://github.com/edanuff).

### Features
- Cycle accurate, used the original schematics to recreate the discrete logic as closely as possible in Verilog
- Uses the [vm80a](https://github.com/1801BM1/vm80a) reverse-engineered 8080a core
- Compatible with .K7 and .CIN tape formats used by the MAME Interact, [DCHector](http://dchector.free.fr/index.html), and [Virtual Interact](http://www.geocities.ws/emucompboy/) emulators
- An [Online Tape Converter](https://interact-tape-converter.netlify.app/) is available for converting tapes to .K7 files
- PS/2 to Interact Keyboard mapping
- Joystick support
- HDMI output

### Roadmap
- SN76477 Sound
- RS232C Peripheral Interface Emulation (MC6850)

### Install
- Copy *.rbf to the root of SD card.<br/>
- Rename the Interact ROM file to boot.rom and place in games/Interact<br/>
- Place .K7 or .CIN files in games/Interact<br/>
