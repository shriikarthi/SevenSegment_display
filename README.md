Exp-No: 02 - Write and simulate seven segment display using Verilog HDL and verify with testbench
Aim:

  To design and simulate a Seven Segment using Verilog HDL and verify its functionality through a testbench using the Vivado 2023.1 simulation environment.
Apparatus Required:

  Vivado 2023.1

Procedure:


Launch Vivado Open Vivado 2023.1 by double-clicking the Vivado icon or searching for it in the Start menu.
Create a New Project Click on "Create Project" from the Vivado Quick Start window. In the New Project Wizard: Project Name: Enter a name for the project (e.g., Mux4_to_1). Project Location: Select the folder where the project will be saved. Click Next. Project Type: Select RTL Project, then click Next. Add Sources: Click on "Add Files" to add the Verilog files (e.g., mux4_to_1_gate.v, mux4_to_1_dataflow.v, etc.). Make sure to check the box "Copy sources into project" to avoid any external file dependencies. Click Next. Add Constraints: Skip this step by clicking Next (since no constraints are needed for simulation). Default Part Selection: You can choose a part based on the FPGA board you are using (if any). If no board is used, you can choose any part, for example, xc7a35ticsg324-1L (Artix-7). Click Next, then Finish.
Add Verilog Source Files In the "Sources" window, right-click on "Design Sources" and select Add Sources if you didn't add all files earlier. Add the Verilog files (mux4_to_1_gate.v, mux4_to_1_dataflow.v, etc.) and the testbench (mux4_to_1_tb.v).
Check Syntax Expand the "Flow Navigator" on the left side of the Vivado interface. Under "Synthesis", click "Run Synthesis". Vivado will check your design for syntax errors. If any errors or warnings appear, correct them in the respective Verilog files and re-run the synthesis.
Simulate the Design In the Flow Navigator, under "Simulation", click on "Run Simulation" → "Run Behavioral Simulation". Vivado will open the Simulations Window, and the waveform window will show the signals defined in the testbench.
View and Analyze Simulation Results 
Adjust Simulation Time To run a longer simulation or adjust timing, go to the Simulation Settings by clicking "Simulation" → "Simulation Settings". Under "Simulation", modify the Run Time (e.g., set to 1000ns).
Generate Simulation Report Once the simulation is complete, you can generate a simulation report by right-clicking on the simulation results window and selecting "Export Simulation Results". Save the report for reference in your lab records.
Save and Document Results Save your project by clicking File → Save Project. Take screenshots of the waveform window and include them in your lab report to document your results. You can include the timing diagram from the simulation window showing the correct functionality of the Seven Segment across different select inputs and data inputs.
Close the Simulation Once done, by going to Simulation → "Close Simulation

Input/Output Signal Diagram: ![WhatsApp Image 2025-09-12 at 10 18 41_97f8ae1a](https://github.com/user-attachments/assets/2a921a4e-45cd-4ca1-b984-03807aee71bb)


RTL Code:
`timescale 1ns / 1ps

module seven_segment (
    input [3:0] data_in,
    output reg [6:0] segments_out
    );

    // segments_out maps to {g,f,e,d,c,b,a}
    always @(*)
    begin
        case (data_in)
            4'd0: segments_out = 7'b1000000; // 0
            4'd1: segments_out = 7'b1111001; // 1
            4'd2: segments_out = 7'b0100100; // 2
            4'd3: segments_out = 7'b0110000; // 3
            4'd4: segments_out = 7'b0011001; // 4
            4'd5: segments_out = 7'b0010010; // 5
            4'd6: segments_out = 7'b0000010; // 6
            4'd7: segments_out = 7'b1111000; // 7
            4'd8: segments_out = 7'b0000000; // 8
            4'd9: segments_out = 7'b0010000; // 9
            default: segments_out = 7'b1111111; // Off
        endcase
    end

endmodule

TestBench:
`timescale 1ns / 1ps

module seven_segment_tb;

    reg [3:0] tb_data_in;
    wire [6:0] tb_segments_out;

    seven_segment dut (
        .data_in(tb_data_in),
        .segments_out(tb_segments_out)
    );

    initial begin
        tb_data_in = 4'd0;

        // Loop to test all 16 possible inputs
        repeat (16) begin
            #10;
            tb_data_in = tb_data_in + 1;
        end

        #20;
        $finish;
    end

endmodule

Output waveform: ![WhatsApp Image 2025-09-12 at 10 22 51_daff00df](https://github.com/user-attachments/assets/0e8c9927-c213-47a8-9d51-bc1a44a89836)

Conclusion:
A BCD to seven-segment display decoder was successfully designed in Verilog HDL. The design was verified using a testbench that provided all possible 4-bit inputs. The simulation was performed in Vivado, and the output waveform confirmed that the correct 7-bit segment pattern was generated for each valid decimal input (0-9) and that the display was turned off for invalid inputs. The design is functionally correct and ready for implementation.

