Design file:
module traffic_light (
  input clk,
  input rst,
  output reg MG, MY, MR,
  output reg SG, SY, SR
);

  typedef enum reg [1:0] {
    MG_SR = 2'b00,
    MY_SR = 2'b01,
    MR_SG = 2'b10,
    MR_SY = 2'b11
  } state_t;

  state_t state, next_state;
  reg [2:0] timer;

  // State register
  always @(posedge clk or posedge rst) begin
    if (rst) begin
      state <= MG_SR;
      timer <= 0;
    end else begin
      if (timer == 0)
        state <= next_state;
      else
        timer <= timer - 1;
    end
  end

  // Next state logic and outputs
  always @(*) begin
    // Default all lights off
    MG = 0; MY = 0; MR = 0;
    SG = 0; SY = 0; SR = 0;
    next_state = state;
    case (state)
      MG_SR: begin
        MG = 1; SR = 1;
        timer = 5;
        next_state = MY_SR;
      end
      MY_SR: begin
        MY = 1; SR = 1;
        timer = 2;
        next_state = MR_SG;
      end
      MR_SG: begin
        MR = 1; SG = 1;
        timer = 5;
        next_state = MR_SY;
      end
      MR_SY: begin
        MR = 1; SY = 1;
        timer = 2;
        next_state = MG_SR;
      end
    endcase
  end
endmodule


Testbench file:-
module tb_traffic_light;
  reg clk, rst;
  wire MG, MY, MR, SG, SY, SR;

  traffic_light uut (
    .clk(clk), .rst(rst),
    .MG(MG), .MY(MY), .MR(MR),
    .SG(SG), .SY(SY), .SR(SR)
  );

  // Clock: 10ns period
  initial clk = 0;
  always #5 clk = ~clk;

  initial begin
    rst = 1; #10;
    rst = 0;

    #100; // simulate enough cycles to cycle through states
    $finish;
  end
endmodule
