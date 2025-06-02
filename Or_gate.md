Design file:-
module and_gate (
  input a,
  input b,
  output y
);
  assign y = a | b;
endmodule

testbench file :-
module tb_and_gate;
  reg a, b;
  wire y;

  // Instantiate the AND gate
  and_gate uut (
    .a(a),
    .b(b),
    .y(y)
  );

  initial begin
    $display("a b | y");
    a = 0; b = 0; #10;
    $display("%b %b | %b", a, b, y);

    a = 0; b = 1; #10;
    $display("%b %b | %b", a, b, y);

    a = 1; b = 0; #10;
    $display("%b %b | %b", a, b, y);

    a = 1; b = 1; #10;
    $display("%b %b | %b", a, b, y);

    $finish;
  end
endmodule

