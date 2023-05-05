Download Link: https://assignmentchef.com/product/solved-ece253-lab-2-and-switches-lights-and-multiplexers
<br>
The purpose of this exercise is to learn how to connect simple input and output devices to an FPGA chip and implement a circuit that uses these devices. We will use the switches <em>SW</em><sub>9−0 </sub>on the DE1-SoC board as inputs to the circuit. We will use light emitting diodes (LEDs) and 7-segment displays as output devices. Two weeks have been allocated for this lab exercise.

<h1>Preparation</h1>

Week 1: You are required to write the Verilog code for Parts I to III. The lab teaching assistants will mark your preparation for Part III: bring your Verilog code for this part of the lab, pasted into your lab book.

Week 2: You are required to write the Verilog code for Parts IV and V. Part VI is optional. For marking of the preparation by the teaching assistants, you are required to bring with you (pasted into your lab book) your Verilog code for Parts IV and V. You should also show some type of simulation output corresponding to Part V, which illustrates that you made a good attempt to ensure that your code is correct.

<h1>In-lab Work</h1>

Week 1: You are required to implement and test Parts I to III. You will only need to demonstrate Part III to the teaching assistants.

Week 2: You are required to implement, test, and demonstrate to the teaching assistants Parts IV and V.

<h1>Part I</h1>

The DE1-SoC board provides 10 slide switches, called <em>SW</em><sub>9−0</sub>, that can be used as inputs to a circuit, and 10 red lights, called <em>LEDR</em><sub>9−0</sub>, that can be used to display output values. Figure 1 shows a simple Verilog module that uses these switches and shows their states on the LEDs. Since there are 10 switches and lights it is convenient to represent them as vectors in the Verilog code, as shown. We have used a single assignment statement for all 10 <em>LEDR </em>outputs, which is equivalent to the individual assignments

assign LEDR[9] = SW[9]; assign LEDR[8] = SW[8];

<em>…</em>

assign LEDR[0] = SW[0];

The DE1-SoC board has hardwired connections between its FPGA chip and the switches and lights. To use <em>SW</em><sub>9−0 </sub>and <em>LEDR</em><sub>9−0 </sub>it is necessary to include in your Quartus II project the correct pin assignments, which are given in the <em>DE1-SoC User Manual</em>. For example, the manual specifies that on the DE1-SoC board <em>SW</em><sub>0 </sub>is connected to the FPGA pin <em>AB12 </em>and <em>LEDR</em><sub>0 </sub>is connected to pin <em>V16</em>. A good way to make the required pin assignments is to import into the Quartus II software the file called <em>DE1-SoC.qsf</em>.

The pin assignments in the <em>.qsf </em>file are useful only if the pin names given in the file are exactly the same as the port names used in your Verilog module. The file uses the names <em>SW</em>[0] <em>… SW</em>[9] and <em>LEDR</em>[0] <em>… LEDR</em>[9] for the switches and lights, which is the reason we used these names in Figure 1.

// Simple module that connects the SW switches to the LEDR lights

module part1 (SW, LEDR);

input [9:0] SW;      // toggle switches output [9:0] LEDR; // red LEDs

assign LEDR = SW;

<h1>endmodule</h1>

Figure 1. Verilog code that uses the DE1-SoC board switches and lights.

Perform the following steps to implement a circuit corresponding to the code in Figure 1 on the DE1-SoC board.

<ol>

 <li>Create a new Quartus II project for your circuit. For the Altera DE1-SoC board, select Cyclone V 5CSEMA5F31C6 as the target chip.</li>

 <li>Type the Verilog code from Figure 1 into a file, and include it in your project.</li>

 <li>Include in your project the required pin assignments for the DE1-SoC board, as discussed above. Compilethe project.</li>

 <li>Download the compiled circuit into the FPGA chip. Test the functionality of the circuit by toggling theswitches and observing the LEDs.</li>

</ol>

<h1>Part II</h1>

Figure 2<em>a </em>shows a sum-of-products circuit that implements a 2-to-1 <em>multiplexer </em>with a select input <em>s</em>. If <em>s </em>=0 the multiplexer’s output <em>m </em>is equal to the input <em>x</em>, and if <em>s </em>= 1 the output is equal to <em>y</em>. Part <em>b </em>of the figure gives a truth table for this multiplexer, and part <em>c </em>shows its circuit symbol.

<ol>

 <li>Circuit</li>

</ol>

<table width="261">

 <tbody>

  <tr>

   <td width="105">


    <table width="55">

     <tbody>

      <tr>

       <td width="28"><em>s</em></td>

       <td width="27"><em>m</em></td>

      </tr>

      <tr>

       <td width="28">01</td>

       <td width="27"><em>x y</em></td>

      </tr>

     </tbody>

    </table></td>

   <td width="156"></td>

  </tr>

 </tbody>

</table>

<ol>

 <li>Truth table c) Symbol</li>

</ol>

Figure 2. A 2-to-1 multiplexer.

The multiplexer can be described by the following Verilog statement:

assign m = (∼s &amp; x) | (s &amp; y);

You are to write a Verilog module that includes four assignment statements like the one shown above to describe the circuit given in Figure 3<em>a</em>. This circuit has two four-bit inputs, <em>X </em>and <em>Y </em>, and produces the four-bit output <em>M</em>. If <em>s </em>=0 then <em>M </em>= <em>X</em>, while if <em>s </em>=1 then <em>M </em>= <em>Y </em>. We refer to this circuit as a four-bit wide 2-to-1 multiplexer.

It has the circuit symbol shown in Figure 3<em>b</em>, in which <em>X</em>, <em>Y </em>, and <em>M </em>are depicted as four-bit wires.

<ol>

 <li>a) Circuit b) Symbol</li>

</ol>

Figure 3. A four-bit wide 2-to-1 multiplexer.

Perform the steps below.

<ol>

 <li>Create a new Quartus II project for your circuit.</li>

 <li>Include your Verilog file for the four-bit wide 2-to-1 multiplexer in your project. Use switch <em>SW</em><sub>9 </sub>on the DE1-SoC board as the <em>s </em>input, switches <em>SW</em><sub>3−0 </sub>as the <em>X </em>input and <em>SW</em><sub>7−4 </sub>as the <em>Y </em> Display the value of <em>s </em>on <em>LEDR</em><sub>9</sub>, connect the output <em>M </em>to <em>LEDR</em><sub>3−0</sub>, and connect the unused LEDR lights to the constant value 0.</li>

</ol>

Your Verilog code will be more readable if you use assignment statements of the form

<ul>

 <li>··</li>

</ul>

assign M[0] = (∼s &amp; X[0]) | (s &amp; Y[0]); assign M[1] = (∼s &amp; X[1]) | (s &amp; Y[1]);

<ul>

 <li>··</li>

</ul>

and then use separate assignment statements to associate <em>s</em>, <em>X</em>, and <em>Y </em>to <em>SW </em>switches, and to assign <em>s </em>and <em>M </em>to <em>LEDR </em>lights.

<ol start="3">

 <li>Include in your project the required pin assignments for the DE1-SoC board. As discussed in Part I, theseassignments ensure that the input ports of your Verilog code will use the pins on the FPGA that are connected to the <em>SW </em>switches, and the output ports of your Verilog code will use the FPGA pins connected to the <em>LEDR </em></li>

 <li>Compile the project.</li>

 <li>Download the compiled circuit into the FPGA chip. Test the functionality of the four-bit wide 2-to-1 multiplexer by toggling the switches and observing the LEDs.</li>

</ol>

<h1>Part III</h1>

In Figure 2 we showed a 2-to-1 multiplexer that selects between the two inputs <em>x </em>and <em>y</em>. For this part consider a circuit in which the output <em>m </em>has to be selected from three inputs <em>u</em>, <em>v</em>, and <em>w</em>. Part <em>a </em>of Figure 4 shows how we can build the required 3-to-1 multiplexer by using two 2-to-1 multiplexers. The circuit uses a 2-bit select input <em>s</em><sub>1</sub><em>s</em><sub>0 </sub>and implements the truth table shown in Figure 4<em>b</em>. A circuit symbol for this multiplexer is given in part <em>c </em>of the figure.

Recall from Figure 3 that a four-bit wide 2-to-1 multiplexer can be built by using four instances of a 2-to-1 multiplexer. Figure 5 applies this concept to define a two-bit wide 3-to-1 multiplexer. It contains two instances of the circuit in Figure 4<em>a</em>.

<ol>

 <li>Circuit</li>

</ol>

<table width="347">

 <tbody>

  <tr>

   <td width="129">


    <table width="85">

     <tbody>

      <tr>

       <td width="55"><em>s</em>1 <em>s</em>0</td>

       <td width="31"><em>m</em></td>

      </tr>

      <tr>

       <td width="55">0 00 1</td>

       <td width="31"><em>u</em><em>v</em></td>

      </tr>

      <tr>

       <td width="55">1 01 1</td>

       <td width="31"><em>w w</em></td>

      </tr>

     </tbody>

    </table></td>

   <td width="218"></td>

  </tr>

 </tbody>

</table>

<ol>

 <li>Truth table c) Symbol</li>

</ol>

Figure 4. A 3-to-1 multiplexer.

Figure 5. A two-bit wide 3-to-1 multiplexer.

Perform the following steps to implement the two-bit wide 3-to-1 multiplexer.

<ol>

 <li>Create a new Quartus II project for your circuit.</li>

 <li>Create a Verilog module for the two-bit wide 3-to-1 multiplexer. Connect its select inputs to switches<em>SW</em><sub>9−8</sub>, and use switches SW<sub>5−0 </sub>to provide the three 2-bit inputs <em>U </em>to <em>W</em>. Connect the output <em>M </em>to the red lights <em>LEDR</em><sub>1−0</sub>.</li>

 <li>Include in your project the required pin assignments for the DE1-SoC board. Compile the project.</li>

 <li>Download the compiled circuit into the FPGA chip. Test the functionality of the two-bit wide 3-to-1 multiplexer by toggling the switches and observing the LEDs. Ensure that each of the inputs <em>U </em>to <em>W </em>can be properly selected as the output <em>M</em>.</li>

</ol>

<h1>Part IV</h1>

Figure 6 shows a <em>7-segment </em>decoder module that has the two-bit input <em>c</em><sub>1</sub><em>c</em><sub>0</sub>. This decoder produces seven outputs that are used to display a character on a 7-segment display. Table 1 lists the characters that should be displayed for each valuation of <em>c</em><sub>1</sub><em>c</em><sub>0</sub>. Three characters are included plus the ‘blank’ character, which is selected for code 11.

The seven segments in the display are identified by the indices 0 to 6 shown in the figure. Each segment is illuminated by driving it to the logic value 0. You are to write a Verilog module that implements a logic function for each of the seven segments. Use only simple Verilog assign statements in your code to specify each logic function using a Boolean expression.

Figure 6. A 7-segment decoder.

<table width="107">

 <tbody>

  <tr>

   <td width="39"><em>c</em>1<em>c</em>0</td>

   <td width="68">Character</td>

  </tr>

  <tr>

   <td width="39">00</td>

   <td width="68">d</td>

  </tr>

  <tr>

   <td width="39">01</td>

   <td width="68">E</td>

  </tr>

  <tr>

   <td width="39">1011</td>

   <td width="68">1</td>

  </tr>

 </tbody>

</table>

Table 1. Character codes.

Perform the following steps:

<ol>

 <li>Create a new Quartus II project for your circuit.</li>

 <li>Create a Verilog module for the 7-segment decoder. Connect the <em>c</em><sub>1</sub><em>c</em><sub>0 </sub>inputs to switches <em>SW</em><sub>1−0</sub>, and connect the outputs of the decoder to the <em>HEX0 </em>display on the DE1-SoC board. The segments in this display are called <em>HEX0</em><sub>0</sub>, <em>HEX0</em><sub>1</sub>, <em>…</em>, <em>HEX0</em><sub>6</sub>, corresponding to Figure 6. You should declare the 7-bit port</li>

</ol>

output [0:6] HEX0;

in your Verilog code so that the names of these outputs match the corresponding names in the <em>DE1-SoC User Manual </em>and the pin assignments file.

<ol start="3">

 <li>After making the required DE1-SoC board pin assignments, compile the project.</li>

 <li>Download the compiled circuit into the FPGA chip. Test the functionality of the circuit by toggling the<em>SW</em><sub>1−0 </sub>switches and observing the 7-segment display.</li>

</ol>

<h1>Part V</h1>

Consider the circuit shown in Figure 7. It uses a two-bit wide 3-to-1 multiplexer to enable the selection of three characters that are displayed on a 7-segment display. Using the 7-segment decoder from Part IV this circuit can display the characters d, E, 1, and ‘blank’. The character codes are set according to Table 1 by using the switches <em>SW</em><sub>5−0</sub>, and a specific character is selected for display by setting the switches <em>SW</em><sub>9−8</sub>.

An outline of the Verilog code that represents this circuit is provided in Figure 8. Note that we have used the circuits from Parts III and IV as subcircuits in this code. You are to extend the code in Figure 8 so that it uses three 7-segment displays rather than just one. You will need to use three instances of each of the subcircuits. The purpose of your circuit is to display any word on the four displays that is composed of the characters in Table 1, and be able to rotate this word in a circular fashion across the displays when the switches <em>SW</em><sub>9−8 </sub>are toggled. As an example, if the displayed word is dE1, then your circuit should produce the output patterns illustrated in Table 2.

Figure 7. A circuit that can select and display one of three characters.

Perform the following steps.

<ol>

 <li>Create a new Quartus II project for your circuit.</li>

 <li>Include your Verilog module in the Quartus II project. Connect the switches <em>SW</em><sub>9−8 </sub>to the select inputs of each of the three instances of the two-bit wide 3-to-1 multiplexers. Also connect <em>SW</em><sub>5−0 </sub>to each instance of the multiplexers as required to produce the patterns of characters shown in Table 2. Connect the SW switches to the red lights LEDR, and connect the outputs of the three multiplexers to the 7-segment displays <em>HEX2</em>, <em>HEX1</em>, and <em>HEX0</em>.</li>

 <li>Include the required pin assignments for the DE1-SoC board for all switches, LEDs, and 7-segment displays.Compile the project.</li>

 <li>Download the compiled circuit into the FPGA chip. Test the functionality of the circuit by setting the propercharacter codes on the switches SW<sub>5−0 </sub>and then toggling <em>SW</em><sub>9−8 </sub>to observe the rotation of the characters.</li>

</ol>

module part5 (SW, LEDR, HEX0);

input [9:0] SW;      // slide switches output [9:0] LEDR; // red lights output [0:6] HEX0;             // 7-seg display

wire [1:0] M0;

mux_2bit_3to1 U0 (SW[9:8], SW[5:4], SW[3:2], SW[1:0], M0); char_7seg H0 (M0, HEX0);

<em>…</em>

<h1>endmodule</h1>

// implements a 2-bit wide 3-to-1 multiplexer module mux_2bit_3to1 (S, U, V, W, M);

input [1:0] S, U, V, W; output [1:0] M;

<em>… </em>code not shown endmodule

// implements a 7-segment decoder for d, E, 1 and ‘blank’ module char_7seg (C, Display);

input [1:0] C;                 // input code

output [0:6] Display;       // output 7-seg code <em>… </em>code not shown endmodule

Figure 8. Verilog code for the circuit in Figure 7.

<table width="126">

 <tbody>

  <tr>

   <td width="53"><em>SW</em>9−8</td>

   <td width="73">Characters</td>

  </tr>

  <tr>

   <td width="53">00</td>

   <td width="73">d      E      1</td>

  </tr>

  <tr>

   <td width="53">01</td>

   <td width="73">E      1      d</td>

  </tr>

  <tr>

   <td width="53">10</td>

   <td width="73">1      d      E</td>

  </tr>

 </tbody>

</table>

Table 2. Rotating the word dE1 on three displays.

<h1>Part VI</h1>

Extend your design from Part V so that is uses all six 7-segment displays on the DE1-SoC board. Your circuit needs to display the word dE1 on the six displays and to be able to rotate this word from right-to-left as shown in Table 3. To do this, you will need to connect two-bit wide 6-to-1 multiplexers to each of six 7-segment display decoders. You will need to use three select lines for each of the 6-to-1 multiplexers: connect the select lines to switches <em>SW</em><sub>9−7</sub>.

<table width="198">

 <tbody>

  <tr>

   <td width="53"><em>SW</em>9−7</td>

   <td width="26"> </td>

   <td colspan="2" width="102">Character pattern</td>

   <td width="16"> </td>

  </tr>

  <tr>

   <td width="53">000</td>

   <td width="26"> </td>

   <td width="54"> </td>

   <td width="48">d        E</td>

   <td width="16">1</td>

  </tr>

  <tr>

   <td width="53">001</td>

   <td width="26"> </td>

   <td width="54">d</td>

   <td width="48">E        1</td>

   <td width="16"> </td>

  </tr>

  <tr>

   <td width="53">010</td>

   <td width="26"> </td>

   <td width="54">d          E</td>

   <td width="48">1</td>

   <td width="16"> </td>

  </tr>

  <tr>

   <td width="53">011</td>

   <td width="26">d</td>

   <td width="54">E          1</td>

   <td width="48"> </td>

   <td width="16"> </td>

  </tr>

  <tr>

   <td width="53">100</td>

   <td width="26">E</td>

   <td width="54">1</td>

   <td width="48"> </td>

   <td width="16">d</td>

  </tr>

  <tr>

   <td width="53">101</td>

   <td width="26">1</td>

   <td width="54"> </td>

   <td width="48">d</td>

   <td width="16">E</td>

  </tr>

 </tbody>

</table>

Table 3. Rotating the word dE1 on six displays.

Perform the following steps:

<ol>

 <li>Create a new Quartus II project for your circuit.</li>

 <li>Include your Verilog module in the Quartus II project. Connect the switches <em>SW</em><sub>9−7 </sub>to the select inputs of each instance of the multiplexers in your circuit. Also connect <em>SW</em><sub>5−0 </sub>to each instance of the multiplexers as required to produce the patterns of characters shown in Table 3. (Hint: for some inputs of the multiplexers you will want to select the ‘blank’ character.) Connect the outputs of your multiplexers to the 7-segment displays <em>HEX5</em>, <em>…</em>, <em>HEX0</em>.</li>

 <li>Include the required pin assignments for the DE1-SoC board for all switches, LEDs, and 7-segment displays.Compile the project.</li>

 <li>Download the compiled circuit into the FPGA chip. Test the functionality of the circuit by setting the propercharacter codes on the switches SW<sub>5−0 </sub>and then toggling <em>SW</em><sub>9−7 </sub>to observe the rotation of the characters.</li>

</ol>