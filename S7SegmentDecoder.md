Design file:-
module seven_seg_decoder (
  input [3:0] bin,
  output reg [6:0] seg
);
  always @(*) begin
    case (bin)
      4'd0: seg = 7'b1111110;
      4'd1: seg = 7'b0110000;
      4'd2: seg = 7'b1101101;
      4'd3: seg = 7'b1111001;
      4'd4: seg = 7'b0110011;
      4'd5: seg = 7'b1011011;
      4'd6: seg = 7'b1011111;
      4'd7: seg = 7'b1110000;
      4'd8: seg = 7'b1111111;
      4'd9: seg = 7'b1111011;
      default: seg = 7'b0000001; // display dash for invalid input
    endcase
  end
endmodule


Testbench file:-
module tb_seven_seg_decoder;
  reg [3:0] bin;
  wire [6:0] seg;

  seven_seg_decoder uut (
    .bin(bin),
    .seg(seg)
  );

  initial begin
    $display("bin | seg");
    for (bin = 0; bin < 16; bin = bin + 1) begin
      #10;
      $display("%2d  | %b", bin, seg);
    end
    $finish;
  end
endmodule
