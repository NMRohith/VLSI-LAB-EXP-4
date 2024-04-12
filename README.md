# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

## AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

## APPARATUS REQUIRED:
Xilinx 14.7
Spartan6 FPGA

## PROCEDURE:
STEP:1  Start  the Xilinx navigator, Select and Name the New project.       
STEP:2  Select the device family, device, package and speed.            
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                              
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.       
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                              
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.                      
STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.       
STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained.        
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.       
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.       
STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.       

## SR FLIPFLOP
### Logic diagram:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)
## Verilog code:
```
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
```
### Output waveform:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/ef9e2271-8554-4d91-8aca-0d29872a7ecd)
## JK FLIPFLOP
### Logic diagram:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/45fd07eb-9d17-4d3e-a3e2-f167a14896f7)
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

### Verilog code:
```
module jkff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({j,k})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=~q;
endcase
end
end
endmodule
```
### Output waveform:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/bea80070-d30d-4226-9a5b-01898f72e01d)

## T FLIPFLOP
### Logic diagram:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/9efc832c-e4b2-42b1-8afd-25fc1b4ee127)
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)

### Verilog code:
```
module tff(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
```
### Output waveform:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/8419bbf3-b055-4011-a4cf-778debb8d285)

## D FLIPFLOP
### Logic diagram:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/4f774604-20d2-485d-9079-5592929c34df)

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)

### Verilog code:
```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
```
### Output waveform:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/4a8ef8b3-248c-4693-ab35-9ff8f6500341)

## COUNTER
## Updown Counter:
### Logic diagram:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/23c97c73-4bc9-48b6-95a7-5c70426be6b4)
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)
### Verilog code:
```
module udc(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```
### Output waveform:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/d314575c-1f83-45ae-8381-e1c37ec1f402)
## Mod-10 Counter:
### Logic diagram:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/c4dfc8cd-9bc1-4eaa-b8e3-e50537cd864a)

### Verilog code:
```
module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
```
### Output waveform:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/8bc92aaa-b84e-49dc-b943-4c2a688a0096)
## RIPPLE CARRY COUNTER:
### Logic Diagram:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/5d1443c7-1b1a-4801-9ebd-10b6f38b8ca8)
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/0984d8fd-3404-4384-a996-929c90dfa836)

### Verilog code:
```
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule

module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule

module rcc(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf1(q[0],clk,rst);
tff tf2(q[1],q[0],rst);
tff tf3(q[2],q[1],rst);
tff tf4(q[3],q[2],rst);
endmodule
```
### Output Waveform:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/163638659/f80d72c6-14a2-472d-9d60-fa78bc968561)

## Result:
Hence SR, JK, T, D - FLIPFLOP, COUNTER DESIGN are simulated and synthesised using Xilinx ISE.

