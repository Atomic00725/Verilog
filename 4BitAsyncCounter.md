Design File:-

module async_counter (
  input clk,
  input rst,
  output [3:0] q
);

  wire q0, q1, q2, q3;

  // Toggle flip-flops
  t_flip_flop tff0 (.clk(clk),   .rst(rst), .q(q0));
  t_flip_flop tff1 (.clk(q0),    .rst(rst), .q(q1));
  t_flip_flop tff2 (.clk(q1),    .rst(rst), .q(q2));
  t_flip_flop tff3 (.clk(q2),    .rst(rst), .q(q3));

  assign q = {q3, q2, q1, q0};

endmodule

// T flip-flop: toggles on each clock
module t_flip_flop (
  input clk,
  input rst,
  output reg q
);
  always @(posedge clk or posedge rst) begin
    if (rst)
      q <= 0;
    else
      q <= ~q;
  end
endmodule

Testbench file:-


`timescale 1ns/1ps

module tb_async_counter;
  reg clk, rst;
  wire [3:0] q;

  async_counter uut (.clk(clk), .rst(rst), .q(q));

  initial clk = 0;
  always #5 clk = ~clk;

  initial begin
    $dumpfile("wave.vcd");
    $dumpvars(0, tb_async_counter);
    $monitor("Time=%0t | rst=%b | q=%b", $time, rst, q);

    rst = 1; #10;
    rst = 0;

    #200;
    $finish;
  end
endmodule
