# esim_mxd_soc_crkt
</br>

# Implementation of Cmos Buffer Along With Multiplexer with Adder/Subtractor for Signal Shaping Operation
</br>



</br>




This repository gives a detailed report on the design of a Implementation of Cmos Buffer Along With Multiplexer with Adder/Subtractor for Signal Shaping Operation using open-source EDA tools and skywater130nm PDK . The simulation being carried out is in mixed-mode (i.e.) both analog and digital simulation. Later the obtained simulation, is verified for it's correctness and functionality.

 
<br>

#  Table of Contents

* [Introduction](#-Introduction) 
* [Cmos Buffer Along With Multiplexer with Adder/Subtractor for Signal Shaping Operation](#-Cmos-Buffer-Along-With-Multiplexer-with-Adder/Subtractor-for-Signal-Shaping-Operation)
* [Software Tools Used](#-Software-Tools-Used) 
* [Implemented Circuit Design using eSim](#-Implemented-Circuit-Design-using-eSim) 
    * [Schematics](#-Schematics) 
    * [Verilog_codes](#-Verilog-codes)
* [Resultant Waveforms](#-Resultant-Waveforms) 
* [Netlist](#-Netlist)
* [Author](#-Author)
* [Acknowledgements](#-Acknowledgements)



<br>

# 📝 Introduction

 An  sine  wave  generator  along  with cmos  buffer  is  used  to  generate  signals.  Output  is  fed  to  4x1 multiplexer. An Adder/subtractor circuit is design to give either sum  and  carry  or  borrow  and  difference  to  input  signals  for mux. The output of mux signal is AND-ed with input signal for modifing  signal  according  to  mux  output.

 
 </br>

*[Back To Top](#-Table-of-Contents)* ⤴️ 

</br>

# 📝 Cmos Buffer Along With Multiplexer with  Adder/Subtractor for Signal Shaping Operation


Sine  wave  is  generated  passed  to  cmos  buffer  to  generate signals. Half  Adder  is  the  adder  that  adds  two  inputs  and produces  two  outputs.  The  first  2  inputs  are  A  and  B  . The  output  carry is designated  as C-OUT and  the normal output  is designated as  S  which  is  SUM.  A  Half  subtractor  is  a  combinational circuit  that  performs  subtraction  of  2  bits,  one  is  minuend and  other  is  subtrahend,  This  circuit  has  two  inputs  and two  outputs.  The  two  inputs  A,  B  denote  the minuend and  subtrahend   respectively. The   two   outputs,   D   and   Bout   represent   the   difference and  output  borrow,  respectively.  This  output  is  fed  to  4x1Multiplexer.   Multiplexer   is   a   combinational   circuit   which has  maximum  of  2n  data  inputs,  ‘n’  selection  lines  and single  output  line.  Among  these  data  inputs  only  one  will be  connected  to  the  output  based  on  the  select  line  values. So,  a  4x1  mux  have  4  data  input  lines,  2  select  lines  and one  output  line.  So,  based  on  the  output  of  input  signals  the corresponding  data  line  is  connected  to  the  output  line.  This mux output is AND-ed with input signal. So based on select line  either  sum/difference  or  carry/borrow  or  remaining  data lines  will  be  AND-ed  with  input  signal  to  produce  desired output.


# Software Tools Used

<br>

* eSim 

  * eSim is a free and open-sourced EDA tool for circuit design, simulation, analysis and PCB design. It is an integrated tool built using free/libre and open source software such as KiCad, Ngspice, Verilator, makerchip-app, sandpiper-saas and GHDL. eSim is released under GPL.
  
   🔗 https://esim.fossee.in/home


* KiCad

 * KiCad's Schematic Editor supports everything from the most basic schematic to a complex hierarchical design with hundreds of sheets. It helps to create our own custom symbols or use some of the thousands found in the official KiCad library. We can verify our design with integrated SPICE simulator and electrical rules checker.
    
   🔗 https://www.kicad.org/

* Ngspice

 *  Ngspice is a mixed-level/mixed-signal electronic circuit simulator. Ngspice implements three classes of analysis: nonlinear DC analyses, Nonlinear transient analyses, linear AC analyses.

   🔗 http://ngspice.sourceforge.net/
   
* Verilator

 *  Verilator is a free and open-source software tool which converts Verilog code to a cycle-accurate behavioral model in C++ or SystemC.

   🔗 https://www.veripool.org/verilator/
   
* Makerchip

 *  A web-based IDE that is used to design and simulate digital circuits using Verilog, and the language extension of Verilog, TL-Verilog.

   🔗   https://www.makerchip.com/
   
* Skywater PDK

  * The SKY130 is a mature 180nm-130nm hybrid technology originally developed internally by Cypress Semiconductor before being spun out into SkyWater Technology and made accessible to general industry. SkyWater and Google’s collaboration is now making this technology accessible to everyone.

  * The SKY130 Process Node is an extremely flexible offering, including many normally optional features as standard (features like the local interconnect, SONOS functionality, MiM capacitors, and more). This provides the designer with a wide range of flexibility in design choices
   
   
   
 

</br>

*[Back To Top](#-Table-of-Contents)* ⤴️ 

</br>


# 📝 Implemented Circuit Design using eSim

## 📋 Schematics

Schematic 

![bssch](Images/sch.png)

Schematic designed for signal genaration

![bssch](Images/sig.png)

Schematic designed for  4x1 mux and AND gate 

![bssch](Images/s1.png)

Schematic designed for  Adder/Subractor

![bssch](Images/s2.png)

Skymode block

![bssch](Images/sky.png)

## 📋 Verilog Codes

- The digital block is the *sri_mux.v* which is built using the following verilog code
```verilog
module srimux (input wire[3:0] in, input wire[1:0] s, output reg out);

always @ (1)
case(s)

	0 : out = in[0];
	1 : out = in[1];
	2 : out = in[2];
	3 : out = in[3];

endcase
endmodule



```

- The digital block is the *sri_and.v* which is built using the following verilog code
```verilog
module sri_and(output Y, input A, B);
    and(Y, A, B); 
endmodule

```

- The digital block is the *sri_add_sub.v* which is built using the following verilog code
```verilog
module sri_add_sub (a, b, s ,s_d, c_b);
input a, b,s;
output s_d, c_b;
wire x;
  xor u1(s_d,a, b);
  xor u3(x,a, s);
  and u2(c_b,x, b);
endmodule


```



# 📝 Resultant Waveforms

Resultant waveform of Signal Generation

![bstbout](Images/out1.png)

Resultant waveform of Adder/Subractor

![bstbout](Images/out2.png)

Resultant waveform of Cmos Buffer Along With Multiplexer with Adder/Subtractor for Signal Shaping Operation

![bstbout](Images/out3.png)


![bstbout](Images/out4.png)


</br>

*[Back To Top](#-Table-of-Contents)* ⤴️ 

</br>

# 📝 Netlist

The Netlist for the designed circuit is generated after simulating the circuit.

```
* /home/snk/sri/sri.cir

.include "C:\FOSSEE\eSim\library\sky130_fd_pr\models\sky130_fd_pr__model__linear.model.spice"
.include "C:\FOSSEE\eSim\library\sky130_fd_pr\models\sky130_fd_pr__model__r+c.model.spice"
.lib "C:\FOSSEE\eSim\library\sky130_fd_pr\models\sky130.lib.spice" tt
.include "C:\FOSSEE\eSim\library\sky130_fd_pr\models\sky130_fd_pr__model__diode_pw2nd_11v0.model.spice"
.include "C:\FOSSEE\eSim\library\sky130_fd_pr\models\sky130_fd_pr__model__inductors.model.spice"
.include "C:\FOSSEE\eSim\library\sky130_fd_pr\models\sky130_fd_pr__model__diode_pd2nw_11v0.model.spice"
.include "C:\FOSSEE\eSim\library\sky130_fd_pr\models\sky130_fd_pr__model__pnp.model.spice"
xsc2 net-_sc1-pad1_ vin1 gnd gnd sky130_fd_pr__nfet_01v8 
xsc1 net-_sc1-pad1_ vin1 net-_sc1-pad3_ net-_sc1-pad3_ sky130_fd_pr__pfet_01v8 
xsc5 buf_out1 net-_sc1-pad1_ net-_sc1-pad3_ net-_sc1-pad3_ sky130_fd_pr__pfet_01v8 
xsc6 buf_out1 net-_sc1-pad1_ gnd gnd sky130_fd_pr__nfet_01v8 
v1  vin1 gnd sine(0 5 0.5 0 0)
v7  mux3 gnd pulse(0 5 0 0 0 4 8)
* s c m o d e
v3 net-_sc1-pad3_ gnd  dc 1.8
* u1  vin1 plot_v1
* u3  buf_out1 plot_v1
xsc4 net-_sc3-pad1_ vin2 gnd gnd sky130_fd_pr__nfet_01v8 
xsc3 net-_sc3-pad1_ vin2 net-_sc3-pad3_ net-_sc3-pad3_ sky130_fd_pr__pfet_01v8 
xsc7 buf_out2 net-_sc3-pad1_ net-_sc3-pad3_ net-_sc3-pad3_ sky130_fd_pr__pfet_01v8 
xsc8 buf_out2 net-_sc3-pad1_ gnd gnd sky130_fd_pr__nfet_01v8 
v2  vin2 gnd sine(0 5 1 0 0)
v4 net-_sc3-pad3_ gnd  dc 1.8
* u2  vin2 plot_v1
* u4  buf_out2 plot_v1
* u5  s_d c_b net-_u5-pad3_ net-_u5-pad4_ net-_u5-pad5_ net-_u5-pad6_ net-_u13-pad1_ srimux
* u7  net-_u7-pad1_ out dac_bridge_1
* u8  out plot_v1
* u9  net-_u10-pad2_ net-_u13-pad1_ net-_u7-pad1_ sri_and
* u10  f1 net-_u10-pad2_ adc_bridge_1
v5  has1 gnd pulse(0 5 0 0 0 1 2)
v6  has2 gnd pulse(0 5 0.2 0 0 2 4)
v8  has3 gnd pulse(0 5 0 0 0 5 10)
* u11  net-_u11-pad1_ net-_u11-pad2_ net-_u11-pad3_ s_d c_b sri_add_sub
* u12  has1 has2 has3 net-_u11-pad1_ net-_u11-pad2_ net-_u11-pad3_ adc_bridge_3
* u6  mux3 mux3 buf_out1 buf_out2 net-_u5-pad3_ net-_u5-pad4_ net-_u5-pad5_ net-_u5-pad6_ adc_bridge_4
v9  f1 gnd sine(0 5 2 0 0)
* u14  mux_out plot_v1
* u13  net-_u13-pad1_ mux_out dac_bridge_1
* u15  s_d c_b o_s_d o_c_b dac_bridge_2
* u17  o_s_d plot_v1
* u16  o_c_b plot_v1
a1 [s_d c_b net-_u5-pad3_ net-_u5-pad4_ ] [net-_u5-pad5_ net-_u5-pad6_ ] [net-_u13-pad1_ ] u5
a2 [net-_u7-pad1_ ] [out ] u7
a3 [net-_u10-pad2_ ] [net-_u13-pad1_ ] [net-_u7-pad1_ ] u9
a4 [f1 ] [net-_u10-pad2_ ] u10
a5 [net-_u11-pad1_ ] [net-_u11-pad2_ ] [net-_u11-pad3_ ] [s_d ] [c_b ] u11
a6 [has1 has2 has3 ] [net-_u11-pad1_ net-_u11-pad2_ net-_u11-pad3_ ] u12
a7 [mux3 mux3 buf_out1 buf_out2 ] [net-_u5-pad3_ net-_u5-pad4_ net-_u5-pad5_ net-_u5-pad6_ ] u6
a8 [net-_u13-pad1_ ] [mux_out ] u13
a9 [s_d c_b ] [o_s_d o_c_b ] u15
* Schematic Name:                             srimux, NgSpice Name: srimux
.model u5 srimux(rise_delay=1.0e-9 fall_delay=1.0e-9 input_load=1.0e-12 instance_id=1 ) 
* Schematic Name:                             dac_bridge_1, NgSpice Name: dac_bridge
.model u7 dac_bridge(out_low=0.0 out_high=5.0 out_undef=0.5 input_load=1.0e-12 t_rise=1.0e-9 t_fall=1.0e-9 ) 
* Schematic Name:                             sri_and, NgSpice Name: sri_and
.model u9 sri_and(rise_delay=1.0e-9 fall_delay=1.0e-9 input_load=1.0e-12 instance_id=1 ) 
* Schematic Name:                             adc_bridge_1, NgSpice Name: adc_bridge
.model u10 adc_bridge(in_low=1.0 in_high=2.0 rise_delay=1.0e-9 fall_delay=1.0e-9 ) 
* Schematic Name:                             sri_add_sub, NgSpice Name: sri_add_sub
.model u11 sri_add_sub(rise_delay=1.0e-9 fall_delay=1.0e-9 input_load=1.0e-12 instance_id=1 ) 
* Schematic Name:                             adc_bridge_3, NgSpice Name: adc_bridge
.model u12 adc_bridge(in_low=1.0 in_high=2.0 rise_delay=1.0e-9 fall_delay=1.0e-9 ) 
* Schematic Name:                             adc_bridge_4, NgSpice Name: adc_bridge
.model u6 adc_bridge(in_low=1.0 in_high=2.0 rise_delay=1.0e-9 fall_delay=1.0e-9 ) 
* Schematic Name:                             dac_bridge_1, NgSpice Name: dac_bridge
.model u13 dac_bridge(out_low=0.0 out_high=5.0 out_undef=0.5 input_load=1.0e-12 t_rise=1.0e-9 t_fall=1.0e-9 ) 
* Schematic Name:                             dac_bridge_2, NgSpice Name: dac_bridge
.model u15 dac_bridge(out_low=0.0 out_high=5.0 out_undef=0.5 input_load=1.0e-12 t_rise=1.0e-9 t_fall=1.0e-9 ) 
.tran 0.001e-00 10e-00 0e-00

* Control Statements 
.control
run
print allv > plot_data_v.txt
print alli > plot_data_i.txt

plot v(vin1) v(vin2)+11 v(buf_out1)+22 v(buf_out2)+30
plot v(buf_out1) v(buf_out2)+6 v(o_s_d)+12 v(o_c_b)+18 v(mux3)+24 v(mux_out)+30
plot v(has1) v(has2)+6 v(has3)+12 v(o_s_d)+18 v(o_c_b)+24
plot v(mux_out) v(f1)+12 v(out)+20
.endc
.end



```
</br>

*[Back To Top](#-Table-of-Contents)* ⤴️ 

</br>


# Author
 
 🖊️ Srithika S, Second year student, B.E. ECE, Madras Institute of Technology, Anna University, Chennai, India
 
 
#  Acknowledgements

 📖 Kunal Ghosh, Co-Founder of VLSI System Design (VSD) Corp. Pvt. Ltd. - kunalpghosh@gmail.com
 
 📖 Sumanto Kar, eSim Team, FOSSEE
 
 📖 FOSSEE, IIT Bombay
