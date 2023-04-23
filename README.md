Download Link: https://assignmentchef.com/product/solved-ada-homework-4-loopy-tippy
<br>
<h1>Problem A – Loopy Tippy (Programming)</h1>

<h2>Problem Description</h2>

<strong>Background </strong>As you may have learned in class, there is no known algorithm that is able to solve NP-complete problems in polynomial time (yet). However, these problems still happen a lot in real life<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>. One method of solving these problems is to encode them into SAT, i.e., boolean satisfiability problems, and apply existing solvers<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a>. There are several benefits to this approach, such as being able to take advantage of existing, highly optimized solvers, and having more flexibility than domain-specific solvers.

<h3>Story</h3>

I have coined a truly remarkable story about WillyPillow and Chino which this margin is too small to contain.

<h3>Problem Formulation</h3>

You are given a Slitherlink<a href="#_ftn3" name="_ftnref3"><sup>[3]</sup></a> puzzle and <em>Cryptominisat5</em>, a CNF-SAT solver (for which the details are given below). Please solve the puzzle by translating it to CNF-SAT and applying the solver.

In essence, the rules of the puzzle are as follows: you are given a rectangular grid, with each square possibly containing a number. The objective is to color a subset of the edges so that the following conditions are satisfied:

<ol>

 <li>If a square contains a number, the number of colored edges around it needs to be equal to the given number.</li>

 <li>The set of colored edges forms exactly one simple loop.</li>

</ol>

You can try the puzzle out here<a href="#_ftn4" name="_ftnref4"><sup>[4]</sup></a> or (a harder version) here<a href="#_ftn5" name="_ftnref5"><sup>[5]</sup></a>.

<h3>Input Format</h3>

The first line contains two integers <em>r </em>and <em>c</em>, denoting the numbers of rows and columns of the board, respectively. <em>r </em>lines follow, where each line contains <em>c </em>characters representing the board. A character, “.”, corresponds to a square without a number. Note that the given puzzle is guaranteed to have a unique solution.

In addition, since it may be hard to predict the needed time for solving your SAT encoding, it is guaranteed that the puzzles in the subtasks 1 through 5 are sampled from this archive<a href="#_ftn6" name="_ftnref6"><sup>[6]</sup></a>. However, due to a large number of the released test cases, <strong>the upload quota is limited to 5 times a day </strong>to ease the burden on the judge server.

<strong>EDIT:           </strong>It is guaranteed that there is at least one non-zero number on the board.




<strong>Subtask 1, 6 (10% each)</strong>

<ul>

 <li>(<em>r,c</em>) = (3<em>,</em>3)</li>

</ul>

<strong>Subtask 2, 7 (10% each)</strong>

<ul>

 <li>(<em>r,c</em>) = (7<em>,</em>7)</li>

</ul>

<strong>Output Format</strong>

<strong>Subtask 3, 8 (10% each)</strong>

<ul>

 <li>(<em>r,c</em>) = (10<em>,</em>10)</li>

</ul>

<strong>Subtask 4, 9 (10% each)</strong>

<ul>

 <li>(<em>r,c</em>) = (15<em>,</em>15)</li>

</ul>

<strong>Subtask 5, 10 (10% each)</strong>

<ul>

 <li>(<em>r,c</em>) = (20<em>,</em>20)</li>

</ul>

<h3>Bonus (0%)</h3>

<ul>

 <li><em>r,c </em>≤ 128</li>

</ul>




Please print a binary string with (2<em>rc </em>+ <em>r </em>+ <em>c</em>) characters, denoting the answer to the puzzle. The following order shows an example of <em>r </em>= 1<em>,c </em>= 5. The <em>i</em>-th character in your output indicates whether the edge at location <em>i </em>is filled. Specifically, a character “1” denotes that the edge is filled and 0

otherwise.

<strong>Sample Input                                                                  </strong>The human-readable solution to this board is

as follows:

7 7

…..3.

22.3..2

32….2    +-+-+-+-+-+ +-+ .3..2.3    |. . . . .|3|.|

3…..2                                                                                                      +-+-+-+-+ +-


.3132.2                                                                                                       2 2 . 3|. . 2|

3…..3                                                                                                      +-+-+-+-+ +-+-


|3 2 . . .|. 2

<strong>Sample Output                                                          </strong>+-+-+ +-+ +-+-


. 3|.|.|2 . 3|

1111101100001111111010000010                                            <sup>+-+-+ + +-+ +-+</sup>

0111110111000010011010110011                                              <sup>|3 . .|. .|.|2</sup>

1001110010110010110110100000                                             <sup>+-+-+ +-+ + + +</sup>

1011101101001100101011110011                                              <sup>. 3|1 3|2|.|2</sup>

+-+-+ +-+ + +-


(Line breaks added only for clarity; please out- |3 . .|. .|. 3| put the string in one single line.) +-+-+-+ + +-+-+ <strong>Environment</strong>

<em>Cryptominisat5</em><a href="#_ftn7" name="_ftnref7"><sup>[7]</sup></a> is installed on the judge server. Instructions about how to use it can be found on its website. It is recommended that you install the library locally for testing.

On the CSIE workstations, the library (and the cryptominisat5 binary) should be already installed. <strong>Note that you need to compile your program with the flag </strong>-lcryptominisat5<strong>.</strong>

On systems with the proper dependencies (most notably, make and cmake) installed, you can build <em>Cryptominisat5 </em>and compile your program with it by following this screencast<a href="#_ftn8" name="_ftnref8"><sup>[8]</sup></a>.

However, if you have difficulty installing the library, we also provide the following alternative:

Please paste the provided header<a href="#_ftn9" name="_ftnref9"><sup>[9]</sup></a> at the beginning of your source file. The following functions are then provided:

<ul>

 <li>void sat::Init(int n): Initialize the solver with n</li>

 <li>void sat::AddClause(std::vector<em>&lt;</em>int<em>&gt; </em>v): Add a CNF clause that consists of the variables in v. Note that negative numbers denote the negation of a variable (e.g., {1, -2} ⇐⇒ (<em>x</em><sub>1 </sub>∨ ¬<em>x</em><sub>2</sub>)), and thus the variable numbering has to start from 1.</li>

 <li>bool sat::Solve(): Solve the given clauses. Returns true if a solution is found and false otherwise.</li>

 <li>int sat::GetResult(int id): Get the result of the variable id after calling Solve(). Returns 1 if the variable is true, −1 if it is false, and 0 if it is indeterminate.</li>

</ul>

If the macro DIMACS is <em>not </em>defined, the library merely redirects your calls to <em>Cryptominisat</em>. However, if it is defined, then Solve() writes your clauses to out.dimacs in DIMACS format<a href="#_ftn10" name="_ftnref10"><sup>[10]</sup></a> and terminates the program. You can then feed the file to other solvers with standalone binaries, such as <em>Cryptominisat5</em><a href="#_ftn11" name="_ftnref11"><sup>[11]</sup></a>, <em>Microsat</em><a href="#_ftn12" name="_ftnref12"><sup>[12]</sup></a>, <em>Minisat</em><a href="#_ftn13" name="_ftnref13"><sup>[13]</sup></a>, <em>Glucose</em><a href="#_ftn14" name="_ftnref14"><sup>[14]</sup></a>, <em>Lingeling</em><a href="#_ftn15" name="_ftnref15"><sup>[15]</sup></a>, or even browser-based solvers like <em>Minisat.js</em><a href="#_ftn16" name="_ftnref16"><sup>[16]</sup></a>.<a href="#_ftn17" name="_ftnref17"><sup>[17]</sup></a>

<h2>Hints</h2>

<ul>

 <li>Tseytin transformation<sup>18</sup></li>

 <li>Truth table ⇐⇒ CNF</li>

 <li>Incremental SAT<a href="#_ftn18" name="_ftnref18"><sup>[18]</sup></a></li>

 <li>Flood fill</li>

 <li>https://codingnest.com/modern-sat-solvers-fast-neat-underused-part-1-of-n/</li>

 <li>It is possible to solve this <em>without </em>using the solver, but I doubt that it is easier &#x1f642;</li>

</ul>

<h1>Problem B – Reachability Coefficient (Programming)</h1>

<h2>Problem Description</h2>

For two sets <em>X </em>and <em>Y </em>, we define:

You are given a directed acyclic graph <em>G</em>, and for each vertex <em>v</em>, let <em>S</em>(<em>v</em>) be the set of vertices that are reachable from <em>v </em>(vertex <em>u </em>is reachable from vertex <em>v </em>if there exists a simple path from <em>v </em>to <em>u</em>). <em>Q </em>queries in the form of <em>u<sub>i</sub>,v<sub>i </sub></em>are specified, where <em>u<sub>i </sub></em>and <em>v<sub>i </sub></em>are vertices in <em>G</em>. You need to answer <em>f</em>(<em>S</em>(<em>u<sub>i</sub></em>)<em>,S</em>(<em>v<sub>i</sub></em>)), for all given queries.

You are not asked to find the <strong>exact </strong>ratio. Instead, your answer is considered correct if the <strong>absolute error </strong>does not exceed 0<em>.</em>1.

<h2>Input</h2>

The first line of the input contains three integers <em>N,M,Q</em>, representing the number of vertices, the number of edges, and the number of queries, respectively. <em>M </em>lines follow, the <em>i</em>-th of which contains two integers <em>u<sub>i</sub>,v<sub>i</sub></em>, representing a directed edge from the vertex <em>u<sub>i </sub></em>to the vertex <em>v<sub>i</sub></em>. <em>Q </em>lines follow, the <em>i</em>-th of which contains two integers <em>u<sub>i</sub>,v<sub>i</sub></em>, representing a query on the vertex <em>u<sub>i </sub></em>and the vertex <em>v<sub>i</sub></em>.

<ul>

 <li>1 ≤ <em>N </em>≤ 2 × 10<sup>5</sup></li>

 <li>0 ≤ <em>M </em>≤ 3 × 10<sup>5</sup></li>

 <li>1 ≤ <em>Q </em>≤ 2 × 10<sup>5</sup></li>

</ul>

<h2>Output</h2>

Print the answer to each query. Your answer can be considered correct if the <em>absolute error of it to the actual answer does not exceed </em>0<em>.</em>1.

<h3>Test Group 0 (20 %)</h3>

<ul>

 <li>1 ≤ <em>N,Q </em>≤ 1000</li>

 <li>0 ≤ <em>M </em>≤ 5000</li>

</ul>

<strong>Test Group 1 (80 %)</strong>

<ul>

 <li>No other constraints</li>

</ul>

<h2>Sample Input 1</h2>

6 7 5

1 2

<ul>

 <li>3</li>

 <li>3</li>

 <li>4</li>

 <li>5</li>

</ul>

3 5

5 6

<ul>

 <li>3</li>

 <li>4</li>

</ul>

1 6

5 5

2 5

<h2>Sample Output 1</h2>

0.666666666667

0.600000000000

0.166666666667

1.000000000000

0.400000000000

<h2>Hints</h2>

<ul>

 <li>Read the problem statement carefully.</li>

 <li>Read the output section carefully.</li>

</ul>

<h1>Problem C – Yet Another Permutation Problem (Programming) (15 points)</h1>

<h2>Problem Description</h2>

Let <em>S<sub>N </sub></em>be the set of all permutations of length <em>N</em>. Let <em>M<sub>N </sub></em>be the set of all 0-1 matrices of size <em>N </em>×<em>N</em>. We define

<em>f </em>: <em>S<sub>N </sub></em>× <em>M<sub>N </sub></em>→ <em>M<sub>N</sub></em>

with <em>f</em>(<em>p,A</em>)<em><sub>i,j </sub></em>= <em>A<sub>p</sub></em><em><sub>i</sub></em><em>,p<sub>j</sub></em>. That is, the function <em>f </em>interchanges the rows (as well as the columns) of matrix <em>A </em>according to the permutation <em>p</em>.

Let <em>g</em>(<em>A</em>) be the maximum size of the submatrix <em>B </em>of <em>A </em>∈ <em>M<sub>N </sub></em>containing only 1’s such that the diagonal of <em>B </em>lies on the diagonal of <em>A</em>. Formally speaking, <em>g</em>(<em>A</em>) is the maximum <em>r </em>(0 ≤ <em>r </em>≤ <em>N</em>) such that there exists 1 ≤ <em>i </em>≤ <em>N </em>− <em>r </em>+ 1 with the following property:

<em>A<sub>xy </sub></em>= 1<em>, </em>for all <em>i </em>≤ <em>x,y </em>≤ <em>i </em>+ <em>r </em>− 1

Given a <em>N </em>×<em>N </em>0-1 matrix <em>A</em>, please find a permutation <em>p </em>∈ <em>S<sub>N </sub></em>such that <em>g</em>(<em>f</em>(<em>p,A</em>)) is maximized.

<h2>Input</h2>

The first line of the input contains an integer <em>N</em>, indicating the size of the matrix <em>A</em>. <em>N </em>lines follow, the <em>i</em>-th of which contains a string of length <em>N</em>, denoting the <em>i</em>-th row of the matrix <em>A</em>.

<ul>

 <li>1 ≤ <em>N </em>≤ 120</li>

 <li><em>A<sub>ij </sub></em>∈ {0<em>,</em>1}</li>

</ul>

<table width="499">

 <tbody>

  <tr>

   <td width="283"><strong>Test Group 0 (10 %)</strong>•    1 ≤ <em>N </em>≤ 8<strong>Test Group 1 (10 %)</strong>•    1 ≤ <em>N </em>≤ 20</td>

   <td width="215"><strong>Test Group 2 (50 %)</strong>•    1 ≤ <em>N </em>≤ 80<strong>Test Group 3 (30 %)</strong>•    No other constraints.</td>

  </tr>

 </tbody>

</table>

<strong>Output</strong>

Print the optimal permutation <em>p</em>. If there are more than one solutions, any of which will be accepted.

<h2>Sample Input 1</h2>

3

101

000

101

<strong>Sample Output 1</strong>

1 3 2

<h1>Problem D – Hex (Programming)</h1>

<h2>Problem Description</h2>

In this problem, you need to play the game, hex, with the computer. Please read Wikipedia for the rules<a href="#_ftn19" name="_ftnref19"><sup>[19]</sup></a>. In this problem, the <strong>pie rule </strong>(or <strong>swap rule</strong>) is not used.

To try the game online, you can use this site<sup>21</sup>. (Make sure to uncheck <strong>swap rule </strong>first.)

a 11×11 Hex Board that blue wins

To solve this problem, you need to write a program to play with ours. Your program will be accepted if you win <em>Y </em>rounds out of a total of <em>X </em>rounds. You are always the first player.

In your program, you only need to implement two functions:

<ul>

 <li>void init(int n): Start a new game with a nxn board</li>

 <li>std::pair&lt;int, int&gt; decide(std::pair&lt;int, int&gt; p): Decide your move. p is the last move by the opponent. If it is the first move, p would be {-1, -1}. The function should return the position you plan to put you color.</li>

</ul>

The position on the board is represented by a pair(std::pair&lt;int, int&gt; p), where p.first is the index (starting from 0) of the row and p.second is the index (starting from 0) of the column.

<h2>Example Files</h2>

You can download a random sample solution and hex.h at: https://cool.ntu.edu.tw/courses/ 368/files/folder/Homework/Homework4%20Hex

The hex.h file would connect to our server, which is the same AI as the judge. So please send your solution to the judge only if the program already runs correctly at local. <strong>You have a very limited quota per day!</strong>

To compile sample files on Windows, you need to add -lws2_32 in the compiler options.

the index of grids on a board

<h2>Input Limits</h2>

<ul>

 <li>1 ≤ <em>X </em>≤ 20</li>

 <li>1 ≤ <em>Y </em>≤ <em>X</em></li>

 <li>3 ≤ n ≤ 11</li>

 <li>0 ≤ first, q.second <em>&lt; </em>n</li>

</ul>

<h3>Test Group 0 (0 %)</h3>

<h3>Test Group 1 (20 %)</h3>

<h3>Test Group 2 (20 %)</h3>

<h3>Test Group 3 (30 %)</h3>

<h3>Test Group 4 (15 %)</h3>

<h3>Test Group 5 (15 %)</h3>

<h1>Problem E – Magic Wands Linking (Hand-Written) (25 points)</h1>

Have you seen <em>Harry Potter</em>? It is a fantasy story about wizards and magic. Every wizard has a magic wand, and there is a <strong>fitness </strong>value (which is always non-negative) between every pair of wands.

In the fantasy world, there are many phenomenal professors who teach at Hogwarts. Recently, one of the professors invented a new technology called <strong>Magic Wands Linking</strong>, which can greatly enhance the power of wizards. By linking two wands through the technology, both owners can increase their power by the fitness value between the two wands. For example, if a wand <em>w</em><sub>1 </sub>is linked to another wand <em>w</em><sub>2</sub>, and the fitness between <em>w</em><sub>1 </sub>and <em>w</em><sub>2 </sub>is 10, then both the power of <em>w</em><sub>1 </sub>and <em>w</em><sub>2 </sub>is enhanced by 10; the power of the Wizarding World is enhanced by 20 in total. Note that two wands can be linked even if their fitness is 0, but such a linking has no effect on their power. Also, a wand can be linked to more than one wand, and the power enhanced can be accumulated.

However, the technology is not yet mature. The links between the wands should follow the rules below:

<ol>

 <li><strong>RULE1 </strong>There are three attributes of magic wands, <strong>none</strong>, <strong>light</strong>, and <strong>dark</strong>. Initially, all wands are unlinked and have the attribute <strong>none</strong>. If a wand <em>w</em><sub>1 </sub>is linked to another wand <em>w</em><sub>2</sub>, then the two wands must be assigned two opposite attributes, <strong>light </strong>and <strong>dark</strong>. (A wand can only be assigned an attribute once.)</li>

 <li><strong>RULE2 </strong>To maintain the balance of the Wizarding World, the number of light wands and the number of dark wands should be the same.</li>

</ol>

Given <em>N </em>magic wands ({<em>w</em><sub>1</sub><em>,w</em><sub>2</sub><em>,…,w<sub>N</sub></em>}) and <em>M </em>fitness values, can you help the wizards to find the maximum power they can enhance in total? For all of the following questions, you can assume that <em>N </em><strong>is even, </strong><strong>, and the fitness values are always non-negative</strong>.

<ul>

 <li>(4pts) Please solve two problems below.

  <ul>

   <li>(2pts) Assume that:</li>

  </ul></li>

</ul>

N = 4 ({<em>w</em><sub>1</sub><em>,w</em><sub>2</sub><em>,w</em><sub>3</sub><em>,w</em><sub>4</sub>}),

M = 6 ({(<em>w</em><sub>1</sub><em>,w</em><sub>2</sub><em>,</em>5)<em>,</em>(<em>w</em><sub>1</sub><em>,w</em><sub>3</sub><em>,</em>1)<em>,</em>(<em>w</em><sub>1</sub><em>,w</em><sub>4</sub><em>,</em>8)<em>,</em>(<em>w</em><sub>2</sub><em>,w</em><sub>3</sub><em>,</em>1)<em>,</em>(<em>w</em><sub>2</sub><em>,w</em><sub>4</sub><em>,</em>7)<em>,</em>(<em>w</em><sub>3</sub><em>,w</em><sub>4</sub><em>,</em>4)}).

(<em>w</em><sub>1</sub><em>,w</em><sub>2</sub><em>,</em>5) means that the fitness between <em>w</em><sub>1 </sub>and <em>w</em><sub>2 </sub>is 5.

Under RULE1 and RULE2, what is the maximum power they can enhance in total?

Please provide the linking method as well.

<ul>

 <li>(2pts) Following the question (1-1), now assume that we can temporarily <strong>ignore RULE2</strong>. That is, <em>N </em>is still an even number, but the numbers of light wands and dark wands can be different. What is the maximum power they can enhance in total? Please provide the linking method as well.</li>

</ul>

<ul>

 <li>(9pts) Please solve two problems below.

  <ul>

   <li>(4pts) <strong>Maximum Cut Problem</strong>:</li>

  </ul></li>

</ul>

For a graph, a maximum cut is a cut whose size is at least the size of any other cut. The problem of finding a maximum cut in a graph is known as the Maximum Cut Problem. Assuming that Maximum Cut Problem is NP-hard, prove the following problem is NPhard:

<strong>Ignore RULE2</strong>, given <em>N </em>magic wands and <em>M </em>fitness values, find a linking method to enhance the maximum power in total.

<ul>

 <li>(5pts) <strong>Ignore RULE2</strong>, given <em>N </em>magic wands and <em>M </em>fitness values, now consider an approximation algorithm below:</li>

</ul>

Define <em>M<sub>i </sub></em>= {<em>fitness of </em>(<em>w<sub>k</sub>,w<sub>i</sub></em>) | <em>k &lt; i</em>}, <em>W</em><sub>1 </sub>and <em>W</em><sub>2 </sub>as two sets of wands. Initially, set <em>W</em><sub>1 </sub>= {<em>w</em><sub>1</sub>}<em>,W</em><sub>2 </sub>= <em>φ</em>. Then for each <em>i </em>from 2 to <em>N</em>, add <em>w<sub>i </sub></em>to either <em>W</em><sub>1 </sub>or <em>W</em><sub>2</sub>, and link <em>w<sub>i </sub></em>to all wands in the other set, such that the power enhanced in <em>M<sub>i </sub></em>is maximized.

Prove that the above algorithm is a 2-approximation.

<ul>

 <li>(5pts) Now, <strong>under both RULE1 and RULE2 </strong>above, assuming that Maximum Cut Problem and the question (2-1) are NP-hard, prove that the following problem is NP-hard:</li>

</ul>

Given <em>N </em>magic wands and <em>M </em>fitness values, find a linking method to enhance the maximum power in total.

<ul>

 <li>(4pts) The professor who invented Magic Wands Linking realizes that the total power enhanced by linking wands can not be too large, or the Wizarding World will crash due to the power storm! Thus, now he wants to know the minimum power that can be enhanced in total when every wand has at least one linking, and all light wands are linked to all dark wands, so that he can evaluate the feasibility of Magic Wands Linking. However, the problem is harder than he thought.</li>

</ul>

Formally speaking, assuming that Maximum Cut Problem, the question (2-1), and the question (3) are NP-hard, please help him prove that the problem below is NP-hard:

Under both RULE1 and RULE2 above, given <em>N </em>magic wands and <em>M </em>fitness values, find a linking method such that <strong>for each wand </strong><em>w</em><strong>, there exists at least one link to </strong><em>w</em><strong>, and all light wands are linked to all dark wands</strong>, but the total enhanced power is minimized.

<ul>

 <li>(3pts) One week after all magic wands are linked, the Dementors attack Hogwarts suddenly!</li>

</ul>

In order to send wizards to the battlefield, they use two teleportation spells. However, teleportation takes time, so it is better to distribute the wizards evenly to the two spells.

Thus, the problem is:

Assuming that there are <em>N </em>wizards, given <em>N </em>non-negative integers (<em>t</em><sub>1</sub><em>,t</em><sub>2</sub><em>,…,t<sub>N</sub></em>) indicating the time each wizard takes to teleport, please determine whether there is a subset whose sum equals

<em>N </em>to <sup>P </sup><em>t<sub>i</sub>/</em>2.

<em>i</em>=1

Please reduce the <strong>Subset Sum Problem</strong><a href="#_ftn20" name="_ftnref20"><sup>[20]</sup></a> to the problem above in polynomial time.

<h1>Problem F – Band Dream (Hand-Written)</h1>

Kasumi is the leader of the band Poppin’ Party. Because it is the fifth year since Poppin’ Party was created, she wants to create a new song containing continuous melodies of the songs that Poppin’ Party has released before.

For example, if there are two melodies <strong>Do, Re, Mi </strong>and <strong>Mi, Re, Do</strong>. Then <strong>Do, Re, Mi, Re, Do </strong>contains two sub-melodies above but <strong>Do, Re, Do, Mi, Re, Do </strong>does not contain the sub-melody <strong>Do, Re, Mi</strong>.

Because she does not know how to minimize the length of the new song, she wants us to find a song that is <em>short enough </em>in polynomial time.

(1) To solve this problem, we introduce another problem called <strong>Set Cover Problem </strong>and one of its approximate algorithms.

Given a universe of <em>n </em>elements <em>X </em>and a collection of <em>m </em>subsets <em>F </em>= {<em>S</em><sub>1</sub><em>,S</em><sub>2</sub><em>,…,S<sub>m</sub></em>}, where <em>S<sub>i </sub></em>⊂ <em>X </em>for each <em>S<sub>i </sub></em>∈ <em>F</em>. Each <em>S<sub>i </sub></em>has a <strong>positive </strong>cost, denoted as cost(<em>i</em>). The goal is to find a sub-collection <em>C </em>⊂ <em>F </em>of the minimum total cost that covers <em>X</em>, assuming one exists.

<strong>Algorithm 1: </strong>GreedySetCover(X, F)

<ul>

 <li><em>C </em>←− ∅

  <ul>

   <li>Order <em>X </em>as {<em>x</em><sub>1</sub><em>,x</em><sub>2</sub><em>,…,x<sub>n</sub></em>} by the order in which they were covered by the algorithm. If there is more than one element covered in the same iteration, order them arbitrarily. Please show that for each <em>k </em>∈ {1<em>,</em>2<em>,…,n</em>}<em>,</em>price(<em>x<sub>k</sub></em>) <sup>≤ </sup><em><sub>n</sub></em><u><sup>OPT</sup></u><sub>−<em>k</em>+1</sub>, where OPT is the cost of the optimal cover. (4 points)</li>

   <li>Please show that the above algorithm is in polynomial time, and it will obtain a (ln n + <em>O</em>(1))-approximate solution. You can use the result of (1-1) even if you are not able to prove it. (3 points)</li>

  </ul></li>

 <li>The problem that Kasumi wants to solve can be modelled as below: Given a finite set of alphabet Σ, and a set of <em>n </em>strings <em>M </em>= {<em>M</em><sub>1</sub><em>,M</em><sub>2</sub><em>,…,M<sub>n</sub></em>}, where each <em>M<sub>i </sub></em>∈ Σ<sup>∗</sup>. WLOG, assume there is no <em>M<sub>i </sub></em>is sub-string of <em>M<sub>j</sub></em>, for <em>i </em>6= <em>j</em>. Find the shortest string <em>C </em>that contains all sub-strings <em>M<sub>i </sub></em>∈ <em>M</em>. To make things easier, if a string <em>s </em>is a prefix of the string <em>y</em>, and a string <em>t </em>is a suffix of the string <em>y</em>, and <strong>len</strong>(<em>s</em>) + <strong>len</strong>(<em>t</em>) <em>&gt; </em><strong>len</strong>(<em>y</em>), we can call <em>y </em>a possible <strong>merge </strong>of <em>s </em>and <em>t</em>. For example, “abbbc” and “abbbbc” are possible <strong>merge</strong>s of “abbb” and “bbc”, while “abbbbbc”, “abbbbbbc” are all not possible <strong>merge</strong>

  <ul>

   <li>Please show that we can reduce Kasumi’s problem to Set Cover Problem mentioned at the problem (1) in polynomial time, by picking <strong>all strings </strong>and <strong>all possible merges of each pair of strings </strong>in <em>M </em>as the collection <em>F </em>of subsets. You can consider that the length of each string is not more than a constant <em>l</em>. Notice that some <strong>merge</strong>s may contain more than two sub-strings, and this reduction is actually a 2-approximate reduction. (6 points)</li>

   <li>Please show that the solution in (2-1) will obtain a (2 ln n + <em>O</em>(1))-approximate solution.</li>

  </ul></li>

</ul>

You can use the result of (1-2) even if you are not able to prove it. (7 points)

<a href="#_ftnref1" name="_ftn1">[1]</a> E.g., <em>lock-chart solving </em>and <em>dependency management</em>.

<a href="#_ftnref2" name="_ftn2">[2]</a> Usually based on conflict-driven clause learning (https://en.wikipedia.org/wiki/Conflict-driven clause learning), a fascinating algorithm worth reading about.

<a href="#_ftnref3" name="_ftn3">[3]</a> https://en.wikipedia.org/wiki/Slitherlink

<a href="#_ftnref4" name="_ftn4">[4]</a> https://www.chiark.greenend.org.uk/~sgtatham/puzzles/js/loopy.html

<a href="#_ftnref5" name="_ftn5">[5]</a> https://kwontomloop.com/

<a href="#_ftnref6" name="_ftn6">[6]</a> https://www.csie.ntu.edu.tw/~b07902134/ada-19hw4p1-public.zip

<a href="#_ftnref7" name="_ftn7">[7]</a> https://www.msoos.org/cryptominisat5/

<a href="#_ftnref8" name="_ftn8">[8]</a> https://asciinema.org/a/oRbZ9UjnWL36RfEZocJYmCyVZ

<a href="#_ftnref9" name="_ftn9">[9]</a> https://gist.github.com/WillyPillow/a5b4f12faefd66c7ce42690668c002b5

<a href="#_ftnref10" name="_ftn10">[10]</a> https://en.wikipedia.org/wiki/Boolean satisfiability problem#SAT problem format

<a href="#_ftnref11" name="_ftn11">[11]</a> Binaries for Windows and Linux can be found at https://github.com/msoos/cryptominisat/releases.

<a href="#_ftnref12" name="_ftn12">[12]</a> https://github.com/marijnheule/microsat

<a href="#_ftnref13" name="_ftn13">[13]</a> http://minisat.se/

<a href="#_ftnref14" name="_ftn14">[14]</a> https://www.labri.fr/perso/lsimon/glucose/

<a href="#_ftnref15" name="_ftn15">[15]</a> http://fmv.jku.at/lingeling/

<a href="#_ftnref16" name="_ftn16">[16]</a> http://jgalenson.github.io/research.js/demos/minisat.html

<a href="#_ftnref17" name="_ftn17">[17]</a> Other solvers can be found at https://en.wikipedia.org/wiki/Boolean satisfiability problem#External links. 18

https://en.wikipedia.org/wiki/Tseytin transformation

<a href="#_ftnref18" name="_ftn18">[18]</a> https://baldur.iti.kit.edu/sat-competition-2016/index.php?cat=incremental

<a href="#_ftnref19" name="_ftn19">[19]</a> https://en.wikipedia.org/wiki/Hex (board game)#Game play <sup>21</sup>http://www.lutanho.net/play/hex.html

<a href="#_ftnref20" name="_ftn20">[20]</a> Given <em>n </em>non-negative integers (<em>a</em><sub>1</sub><em>,a</em><sub>2</sub><em>,…a<sub>n</sub></em>) and a positive integer <em>W</em>, the Subset Sum Problem seeks whether there is a subset whose sum equals to <em>W</em>. The Subset Sum Problem is known to be NP-hard.