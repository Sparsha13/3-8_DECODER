# 3-to-8 Decoder using Verilog HDL

## Project Overview

This project involves the design and verification of a 3-to-8 decoder using Verilog HDL. A 3-to-8 decoder is a combinational circuit that takes a 3-bit binary input and activates one of the 8 output lines based on the input combination. The design has been verified using UVM (Universal Verification Methodology) and synthesized using OpenROAD.


## Specifications

 ### Inputs:
in[2:0] (3-bit binary input)

en (Enable signal: 1-bit)

### Outputs:

out[7:0] (8-bit one-hot encoded output)

### Design Architecture

The decoder operates based on a combinational always block.

When en = 1, a case statement determines the output based on the 3-bit input.

If en = 0, all outputs remain 0.

## RTL Code

The Verilog implementation of the 3-to-8 decoder:

module decoder3to8 ( 
 input wire [2:0] in, // 3-bit input 
 input wire 
 en, // Enable signal 
 output reg [7:0] out // 8-bit output 
 ); 
always @ (*) begin 
 if (en) begin 
  case (in) 
   3'b000: out = 8'b00000001; 
   3'b001: out = 8'b00000010; 
   3'b010: out = 8'b00000100; 
   3'b011: out = 8'b00001000; 
   3'b100: out = 8'b00010000; 
   3'b101: out = 8'b00100000; 
   3'b110: out = 8'b01000000; 
   3'b111: out = 8'b10000000; 
   default: out = 8'b00000000; 
  endcase
end 
else 
  begin 
    out = 8'b00000000; 
end
end 
endmodule
## Testbench

A testbench was developed to verify the correctness of the decoder.

module tb_decoder3to8;
    reg [2:0] in;
    reg en;
    wire [7:0] out;
    
    decoder3to8 uut (
        .in(in),
        .en(en),
        .out(out)
    );
    
    initial begin
        $monitor("Time=%0t | in=%b | en=%b | out=%b", $time, in, en, out);
        en = 1;
        in = 3'b000; #10;
        in = 3'b001; #10;
        in = 3'b010; #10;
        in = 3'b011; #10;
        in = 3'b100; #10;
        in = 3'b101; #10;
        in = 3'b110; #10;
        in = 3'b111; #10;
        en = 0;
        in = 3'b010; #10;
        $finish;
    end
    
    initial begin
        $dumpfile("dump.vcd");
        $dumpvars(1);
    end
endmodule

## Simulation & Verification

Simulation Tool: Synopsys VCS 2023.03

Verification Methodology: UVM (Universal Verification Methodology)

Testbench Components:

Monitor: Captures DUT output

Driver: Generates stimulus for the decoder

Scoreboard: Compares expected and actual outputs

Coverage: Measures functional coverage

## Synthesis using OpenROAD

The design was synthesized using the OpenROAD tool with Sky130HD technology.

Performance Metrics:

Power Consumption: 535nW

Design Area: 4662 sq. µm

Timing Slack: 0.77 ns (No setup and hold violations)

## Results & Discussion

The functional verification achieved 100% test case pass rate.

The waveform simulation confirmed the expected outputs.

The GDS layout was successfully generated using OpenROAD.

## References

EDA Playground Simulation: View Simulation

GDS Generation: OpenROAD Implementation



