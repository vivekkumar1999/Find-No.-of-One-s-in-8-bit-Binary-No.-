# Find-No.-of-One-s-in-8-bit-Binary-No.-
Writing a program for finding the number of one's in to given 8 bit binary numbers. 


/* Program for finding No. of One's in 8 bit of binary number  */

module Project_1( input clr,[7:0] x, output [3:0] y);
wire [8:0]w;
supply0 gnd;
    half_adder ha1(.clr(clr),.a(x[0]),.b(x[1]),.sum(w[0]),.carry(w[1]));
    full_adder fa1(.Clr(clr),.A(x[2]),.B(x[3]),.Cin(x[4]),.Sum(w[2]),.Carry(w[3]));
    full_adder fa2(.Clr(clr),.A(x[5]),.B(x[6]),.Cin(x[7]),.Sum(w[4]),.Carry(w[5]));
    two_bit_adder twba1(.clr(clr),.x({w[3],w[2]}),.y({w[5],w[4]}),.z({w[8],w[7],w[6]}));
    three_bit_adder thba(.clr(clr),.a({gnd,w[1],w[0]}),.b({w[8],w[7],w[6]}),.c({y[3],y[2],y[1],y[0]}));
           
endmodule


module three_bit_adder(
    input clr,[2:0] a,b,
    output [3:0] c
    );
    wire [1:0]w;
    half_adder ha1(clr,a[0],b[0],c[0],w[0]);
    full_adder fa1(clr,a[1],b[1],w[0],c[1],w[1]);
    full_adder fa2(clr,a[2],b[2],w[1],c[2],c[3]); 
        
endmodule

module two_bit_adder(clr,x,y,z);
input clr;
input [1:0]x,y;
output [2:0]z;
half_adder hf1(clr,x[0],y[0],z[0],w1);
full_adder fl1(clr,x[1],y[1],w1,z[1],z[2]);

endmodule

module full_adder(Clr,A,B,Cin,Sum,Carry);  
input Clr,A,B,Cin;
output Sum,Carry;
wire w1,w2,w3,w4,w5,w6;
and and1(w1,A,Clr);
and and2(w2,B,Clr);
and and3(w3,Cin,Clr);
half_adder hf1(Clr,w1,w2,w4,w5);
half_adder hf2(Clr,w3,w4,Sum,w6);
or or1(Carry,w5,w6);
endmodule

module half_adder(clr,a,b,sum,carry);
input a,b,clr ;
output sum,carry ;
wire w1,w2;
    and and1(w1,a,clr);  
    and and2(w2,b,clr);
    xor sum1(sum,w1,w2);
    and carry1(carry,w1,w2);
endmodule


