
Design file:-
module reg_4bit (
  input clk,
  input [3:0] d,
  output reg [3:0] q
);
  always @(posedge clk) begin
    q <= d; // Non-blocking assignment (important!)
  end
endmodule

Testbench file:-

module tb_reg_4bit;
  reg clk;
  reg [3:0] d;
  wire [3:0] q;

  reg_4bit uut (
    .clk(clk),
    .d(d),
    .q(q)
  );

  // Clock generator: toggles clk every 5 time units
  initial clk = 0;
  always #5 clk = ~clk;

  initial begin
    $display("Time | clk d    q");

    d = 4'b0001; #10;  // clk rising edge at t=5, t=15...
    $display("%4t |  %b  %b  %b", $time, clk, d, q);

    d = 4'b1010; #10;
    $display("%4t |  %b  %b  %b", $time, clk, d, q);

    d = 4'b1111; #10;
    $display("%4t |  %b  %b  %b", $time, clk, d, q);

    $finish;
  end
endmodule

