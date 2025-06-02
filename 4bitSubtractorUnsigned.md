Design File:-
module subtractor_4bit (
  input  [3:0] a,
  input  [3:0] b,
  output [3:0] diff
);
  assign diff = a - b;
endmodule



Testbench file:-
module tb_subtractor_4bit;
  reg  [3:0] a, b;
  wire [3:0] diff;

  subtractor_4bit uut (
    .a(a),
    .b(b),
    .diff(diff)
  );

  initial begin
    $display("a    - b    = diff");

    a = 4'd5; b = 4'd3; #10;
    $display("%d - %d = %d", a, b, diff);

    a = 4'd3; b = 4'd5; #10;
    $display("%d - %d = %d", a, b, diff); // Will wrap around

    a = 4'd7; b = 4'd7; #10;
    $display("%d - %d = %d", a, b, diff);

    a = 4'd0; b = 4'd1; #10;
    $display("%d - %d = %d", a, b, diff); // Underflow

    $finish;
  end
endmodule
