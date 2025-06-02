Design File:-

module d_flip_flop (
  input clk,
  input rst,     // Active-high synchronous reset
  input d,
  output reg q
);

  always @(posedge clk) begin
    if (rst)
      q <= 0;
    else
      q <= d;
  end

endmodule

Testbench file:-

module tb_d_flip_flop;
  reg clk, rst, d;
  wire q;

  d_flip_flop uut (.clk(clk), .rst(rst), .d(d), .q(q));

  // Clock generation
  initial clk = 0;
  always #5 clk = ~clk;

  initial begin
    $display("Time | rst d q");
    $monitor("Time=%0t | rst=%b d=%b q=%b", $time, rst, d, q);

    rst = 1; d = 0; #10;
    rst = 0;

    d = 1; #10;
    d = 0; #10;
    d = 1; #10;

    $finish;
  end
endmodule


