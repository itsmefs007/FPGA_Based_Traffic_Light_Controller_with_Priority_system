# FPGA_Based_Traffic_Light_Controller_with_Priority_system

1. Project Overview Design and implement a smart traffic light controller on an FPGA that: Manages a four-way intersection (can be adapted for T-junctions). Provides a priority override for emergency vehicles detected via sensors (RFID, IR, microphone, camera, or manual switch). Uses finite state machine (FSM) logic for traffic sequencing. Is coded in Verilog (or VHDL). Is simulated in ModelSim or Vivado and ready for Xilinx Spartan FPGA deployment.

2. System Architecture Functional Modules Clock Divider: Generates slower clock from the FPGA master clock for timing. FSM (Finite State Machine): Controls light transitions (Red, Yellow, Green) for each direction. Priority/Emergency Detection: Emergency vehicle sensor input overrides FSM state. Counter/Timer: Establishes green/yellow/red intervals for each direction. Inputs Lane sensors (manual switches, IR, RFID, microphone, camera, etc.). Emergency override input. Outputs Signals for Red, Yellow, Green lights for each direction.

3. FSM (Finite State Machine) Logic Normal Mode Each lane follows standard traffic sequence based on timer or vehicle presence. Priority (Emergency Override) Mode When emergency detected: Current green phase immediately switches to Red for all lanes except the emergency vehicle's lane. Emergency lane gets Green until vehicle passes or override is released. After priority phase, system resumes normal cycle.

4. Verilog Module Coding

module traffic_light_controller (

input clk,

input reset,

input emergency,             // Emergency detected (sensor/switch)

input [3:0] car_present,     // Sensors for each direction

output [2:0] lights_ns,      // North-South lights (Red-Yellow-Green)


output [2:0] lights_ew       // East-West lights (Red-Yellow-Green));
// Internal registers, FSM states, counters, etc.

// FSM logic for regular and emergency override

endmodule

5. Emergency Detection Mechanism Use a dedicated input pin (e.g., from switch, IR, RFID, etc.) on FPGA board. In simulation, use a testbench to assert the emergency signal at different times.

6. Implementation Steps Verilog Code Development Write the FSM module covering all states and transitions (normal and emergency). Implement the timer/counter logic. Simulation Create a ModelSim/Vivado testbench. Simulate normal cycle, then assert emergency signal and observe correct override behavior. Verify return to normal after emergency clears. FPGA Deployment Target Xilinx Spartan (or compatible) part. Use Vivado: RTL coding, synthesis, implementation, bitstream generation. Download onto board Inputs/Outputs on Board Use slide switches for sensors/emergency simulate. Use LEDs to represent lights for each approach.

7. Example FSM States (Pseudo-State Diagram) State NS Light EW Light Emergency Condition NS_Green Green Red Normal NS_Yellow Yellow Red Normal EW_Green Red Green Normal EW_Yellow Red Yellow Normal Emergency_NS Green Red Emergency detected in NS Emergency_EW Red Green Emergency detected in EW

8. Useful References & Tutorials A step-by-step traffic light controller in Vivado (RTL, testbench, implementation). Verilog traffic light controller projects and codes. Intelligent traffic controller with emergency override on FPGA. Complete papers showing emergency detection logic integrated into traffic phases, with simulation and hardware write-up. FSM construction for adaptable timing and emergency intervention.

9. Hardware Setup Select a Xilinx Spartan board (e.g., Spartan-3E, Spartan-6). Map car_present and emergency inputs to slide switches. Map light outputs to LEDs.
