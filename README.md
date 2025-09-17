# SIMULATION AND IMPLEMENTATION OF 4:1 MULTIPLEXER

## AIM
To design and simulate a 4:1 Multiplexer (MUX) using Verilog HDL in four different modeling styles—Gate-Level, Data Flow, Behavioral, and Structural—and to verify its functionality through a testbench using the Vivado 2023.1 simulation environment. The experiment aims to understand how different abstraction levels in Verilog can be used to describe the same digital logic circuit and analyze their performance.

## APPARATUS REQUIRED
- **Vivado 2023.1**

## Procedure

1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** and give a name (e.g., `Mux4_to_1`).  
3. Add/create your Verilog files and testbench.  
4. Select an FPGA part (e.g., `xc7a35ticsg324-1L`).  
5. Run **Synthesis** to check for errors.  
6. Run **Simulation** → **Run Behavioral Simulation**.  
7. Observe the waveforms of inputs and outputs.  
8. Adjust simulation time if needed (e.g., 1000ns).  
9. Save the project and take screenshots of results.  
10. Close simulation.  

---

## Logic Diagram
![image](https://github.com/user-attachments/assets/d4ab4bc3-12b0-44dc-8edb-9d586d8ba856)

---

## Truth Table
![image](https://github.com/user-attachments/assets/c850506c-3f6e-4d6b-8574-939a914b2a5f)

---

## Verilog Code

### 4:1 MUX Gate-Level Implementation
```verilog
// Gate Level Modelling - Skeleton
module mux_41(I,S,Y);
input [3:0]I;
input[1:0]S;
output Y;
wire [4:1]W;
and g1(W[1],(~S[1]),(~S[0]),I[0]);
and g2(W[2],(~S[1]),S[0],I[1]);
and g3(W[3],S[1],(~S[0]),I[2]);
and g4(W[4],S[1],S[0],I[3]);
or g5(Y,W[1],W[2],W[3],W[4]);
endmodule

```
### 4:1 MUX Gate-Level Implementation- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module mux_41_tb;
reg [3:0]I;
reg [1:0]S;
wire Y;
mux_41 uut(I,S,Y);
initial
begin
I=4'B0001;
S=2'b00;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b01;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b10;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b11;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
$finish;
end 
endmodule
```
## Simulated Output Gate Level Modelling


<img width="692" height="389" alt="image" src="https://github.com/user-attachments/assets/c59f2da2-4632-4e35-98bb-caa6841aee29" />

---
### 4:1 MUX Data flow Modelling
```verilog
// Dataflow Modelling - Skeleton
module mux_41(I,S,Y);
input [3:0]I;
input[1:0]S;
output Y;
wire [4:1]W;
assign W[1]= I[0] & (~S[1]) & (~S[0]);
assign W[2]= I[0] & (~S[1]) & S[0];
assign W[3]= I[0] & S[1] & (~S[0]);
assign W[4]= I[0] & S[1] & S[0];
assign Y= W[1] | W[2] | W[3] | W[4];
endmodule
```
### 4:1 MUX Data flow Modelling- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module mux_41_tb;
reg [3:0]I;
reg [1:0]S;
wire Y;
mux_41 uut(I,S,Y);
initial
begin
I=4'B0001;
S=2'b00;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b01;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b10;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b11;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
$finish;
end 
endmodule
```
## Simulated Output Dataflow Modelling


<img width="692" height="389" alt="image" src="https://github.com/user-attachments/assets/744990da-38d6-40aa-b356-91891291dd77" />


---
### 4:1 MUX Behavioral Implementation
```verilog
module MUX_41(I,S,Y);
input [3:0]I;
input[1:0]S;
output reg Y;
always @(I,S)
    begin
        case(S)
        2'b00:Y=I[0];
        2'b01:Y=I[1];
        2'b10:Y=I[2];
        2'b11:Y=I[3];
        endcase
     end
endmodule
```
### 4:1 MUX Behavioral Modelling- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module mux_41_tb;
reg [3:0]I;
reg [1:0]S;
wire Y;
MUX_41 uut(I,S,Y);
initial
begin
I=4'B1001;
S=2'b00;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b01;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b10;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b11;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
$finish;
end 
endmodule
```
## Simulated Output Behavioral Modelling


<img width="692" height="389" alt="image" src="https://github.com/user-attachments/assets/3a3939f0-7d99-4a15-80fa-1f065cb7d895" />



### 4:1 MUX Structural Implementation

![image](https://github.com/user-attachments/assets/eea81c2c-7dfa-43aa-9cea-1ab4ed54db6c)


```verilog
module mux2_to_1 (
    input wire A,
    input wire B,
    input wire S,
    output wire Y
);
    assign Y = S ? B : A;
endmodule

module mux4_to_1_structural (
    input wire A,
    input wire B,
    input wire C,
    input wire D,
    input wire S0,
    input wire S1,
    output wire Y
);




endmodule
```
### Testbench Implementation
```verilog
`timescale 1ns / 1ps

module mux4_to_1_tb;
    reg A, B, C, D, S0, S1;
    wire Y_gate, Y_dataflow, Y_behavioral, Y_structural;

    

    initial begin
        A = 0; B = 0; C = 0; D = 0; S0 = 0; S1 = 0;

      
        #10 $stop;
    end

   
    end
endmodule
```
## Simulated Output Structural Modelling

_______ Here Paste the Simulated output  ___________

---
### CONCLUSION

In this experiment, a 4:1 Multiplexer was successfully designed and simulated using Verilog HDL across four different modeling styles: Gate-Level, Data Flow, Behavioral, and Structural.The simulation results verified the correct functionality of the MUX, with all implementations producing identical outputs for the given input conditions.

