Download Link: https://assignmentchef.com/product/solved-cs2030s-problem-set-10-streams
<br>
<h1></h1>

<ol>

 <li>Write a method omega with signature LongStream omega(int n) that takes in an int n and returns a IntStream containing the first <em>n </em>omega numbers. We use LongStream in order to work with large integer values.</li>

</ol>

The <em>i</em><sup>th </sup>omega number is the number of distinct prime factors for the number <em>i</em>. The first 10 omega numbers are 0<em>,</em>1<em>,</em>1<em>,</em>1<em>,</em>1<em>,</em>2<em>,</em>1<em>,</em>1<em>,</em>1<em>,</em>2. The isPrime method is given below:

boolean isPrime(int n) { return IntStream .range(2, n)

.noneMatch(x -&gt; n%x == 0);

}

<ol start="2">

 <li>Write a method that returns the first <em>n </em>Fibonacci numbers as a Stream&lt;Integer&gt;.</li>

</ol>

For instance, the first 10 Fibonacci numbers are 1<em>,</em>1<em>,</em>2<em>,</em>3<em>,</em>5<em>,</em>8<em>,</em>13<em>,</em>21<em>,</em>34<em>,</em>55.

<em>Hint</em>: Write an additional Pair class that keeps two items around in the stream

<ol start="3">

 <li>In this question, we shall attempt to parallelize the generation of the Fibonacci sequence. As an example, supose we are given the first <em>k </em>= 4 values of the sequence <em>f</em><sub>1 </sub>to <em>f</em><sub>4</sub>, i.e.</li>

</ol>

1<em>,</em>1<em>,</em>2<em>,</em>3

To generate the next <em>k </em>− 1 values, we observe the following:

<table width="361">

 <tbody>

  <tr>

   <td width="27"><em>f</em><sub>5</sub></td>

   <td width="25">=</td>

   <td width="61"><em>f</em>3 + <em>f</em>4</td>

   <td width="25">=</td>

   <td width="99">1 · <em>f</em>3 + 1 · <em>f</em>4</td>

   <td width="25">=</td>

   <td width="98"><em>f</em>1 · <em>f</em>3 + <em>f</em>2 · <em>f</em>4</td>

  </tr>

  <tr>

   <td width="27"><em>f</em><sub>6</sub></td>

   <td width="25">=</td>

   <td width="61"><em>f</em>4 + <em>f</em>5</td>

   <td width="25">=</td>

   <td width="99">1 · <em>f</em>3 + 2 · <em>f</em>4</td>

   <td width="25">=</td>

   <td width="98"><em>f</em>2 · <em>f</em>3 + <em>f</em>3 · <em>f</em>4</td>

  </tr>

  <tr>

   <td width="27"><em>f</em><sub>7</sub></td>

   <td width="25">=</td>

   <td width="61"><em>f</em>5 + <em>f</em>6</td>

   <td width="25">=</td>

   <td width="99">2 · <em>f</em>3 + 3 · <em>f</em>4</td>

   <td width="25">=</td>

   <td width="98"><em>f</em>3 · <em>f</em>3 + <em>f</em>4 · <em>f</em>4</td>

  </tr>

 </tbody>

</table>

Notice that generating each of the terms <em>f</em><sub>5 </sub>to <em>f</em><sub>7 </sub>only depends on the terms of the given sequence. This actually means that generating the terms can now be done in parallel! In addition, repeated application of the above results in an exponential growth of the Fibonacci sequence.

You are now given the following program fragment:

BigInteger findFibTerm(int n) {

List&lt;BigInteger&gt; fibList = new ArrayList&lt;&gt;();

fibList.add(BigInteger.ONE); fibList.add(BigInteger.ONE);

1

while (fibList.size() &lt; n) { generateFib(fibList);

}

return fibList.get(n-1);

}

<ul>

 <li>Using Java parallel streams, complete the generateFib method such that each method call takes in an initial sequence of <em>k </em>terms and fills it with an additional <em>k </em>− 1 terms. The findFibTerm method calls generateFib repeatedly until the <em>n<sup>th </sup></em>term is generated and returned.</li>

 <li>Using the Instant and Duration classes, determine the time it takes the Fibonacci sequence of <em>n </em>= 50000. Compare the times for sequential and parallel generations.</li>

</ul>