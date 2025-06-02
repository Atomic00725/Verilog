Design File:-
module adder_4bit (
  input  [3:0] a,
  input  [3:0] b,
  output [3:0] sum
);
  assign sum = a + b;
endmodule


testbench file:-
module tb_adder_4bit;
  reg  [3:0] a, b;
  wire [3:0] sum;

  adder_4bit uut (
    .a(a),
    .b(b),
    .sum(sum)
  );

  initial begin
    $display("a    + b    = sum");

    a = 4'd3; b = 4'd2; #10;
    $display("%d + %d = %d", a, b, sum);

    a = 4'd9; b = 4'd4; #10;
    $display("%d + %d = %d", a, b, sum);

    a = 4'd15; b = 4'd1; #10;
    $display("%d + %d = %d", a, b, sum); // watch for overflow

    $finish;
  end
endmodule

