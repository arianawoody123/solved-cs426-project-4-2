Download Link: https://assignmentchef.com/product/solved-cs426-project-4-2
<br>









In this project, you will implement sparse matrix-vector multiplication. You will use CUDA to implement this problem.

<h1>Problem Statement</h1>




This problem concerns multiplication of a sparse matrix with a vector. You have to implement the operation x<sub>i+1</sub> = Ax<sub>i</sub>, where A is your sparse matrix and x is the vector (Store result of the product of A and x into x at the end of i<sup>th</sup> iteration and use it in the i+1<sup>th</sup> iteration).

In this project you have the following data structures:

<strong>x array: </strong>Used to store the vector. <strong>Initialize x to all 1s</strong> before the Matrix-vector product iterations begin.

The sparse matrix is represented using the following three data structures:

<strong>row_ptr array</strong>: For each row <em>i</em> of the sparse matrix, <em>row_ptr[i]</em> contains an index number associated with the first nonzero element in this row. This index can be used in <em>col_ind</em> and <em>values</em> arrays (see below). If row <em>i</em> does not contain a non-zero element (i.e. it is all zeros), then <em>rowptr[i]==rowptr[i+1]</em>.

<strong>col_ind</strong> <strong>array</strong>: This array contains the column indices of the non-zero elements. If the matrix element at row <em>i </em>&amp; column <em>j</em> is a non-zero element, then <em>col_ind[k]==j</em> for some <em>k</em> such that <em>row_ptr[i] &lt;= k &lt;</em> <em>row_ptr[i+1]. </em>

<strong>values array</strong>: This array contains the values of non-zero elements. This array is indexed similar to the <em>col_ind</em> array. If the matrix element at row <em>i</em> column <em>j</em> has the non-zero value <em>v</em>, then for some <em>k</em> such that <em>rowptr[i] &lt;= k &lt; rowptr[i+1]</em>, you have <em>values[k]==v. </em>






















<table width="442">

 <tbody>

  <tr>

   <td width="73">0</td>

   <td width="102">2</td>

   <td width="84">6</td>

   <td width="91">6</td>

   <td width="91">8</td>

  </tr>

 </tbody>

</table>

<strong>(row_ptr array) </strong>

The arrows indicate the relations – for every k in the range row_ptr[i] &lt;= k &lt; row_ptr[i+1], you have col_ind[k]=j such that  A[i][j] is a non zero value and it is stored in values[k].

For example in 0<sup>th</sup> row, column 1 and 7 contain non-zero values 56 and 123 respectively. Other columns in row 0 contain 0s. Row 2 contains all 0s, which is reflected in the fact that <em>row_ptr[2]==row_ptr[3]. </em>Row 4 also contains all zeros, but it is the last row. So <em>row_ptr[4]</em> points somewhere outside <em>col_ind</em> array. (Handle end conditions carefully, take care that you don’t get segmentation faults by accidentally trying to access a <em>row_ptr</em> location that is out of bounds.)

Write a program that uses CUDA that performs the Matrix-vector product. (No need to use CUDA for reading the input, printing etc.) You can assume that the sparse matrix is a square matrix.

The iterations of x<sub>i+1</sub> = Ax<sub>i</sub> could be implemented using the following loop. The time to be noted is the total time required for all the iterations to get over:

<strong>for(iter=0; iter&lt;number_of_iterations; iter++) { matrix-vector computation </strong>

<strong>        } </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<h1>Language</h1>




You should use C language with CUDA (You can refer to course slides for specifications). You may use the following command to compile your files:  <strong>nvcc filename.cu </strong>

<h1>Machines</h1>

You will need to use a machine with NVIDIA GPU card. If you want to use a GPU available in our servers, email <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="036862626d2d62687a6c6f43616a6f68666d772d6667762d7771">[email protected]</a> to ask for an account. Note that, one GPU card cannot be used by two programs at the same time so your timing results will be correct.

<h1>Testing</h1>




<ul>

 <li><strong>Initialize x to all 1s</strong> before the Matrix-vector product iterations begin.</li>

 <li>Your programs should accept as input from the first three command line arguments. – The number of threads used to compute Matrix-vector product

  <ol start="2">

   <li>The number of repetitions and</li>

   <li>An argument to print on stdout (See below).</li>

   <li>Test-file name</li>

  </ol></li>

 <li>The command line argument #3 controls whether or not the program is to print the initial matrix, vector and the resulting vector after all the x<sub>i+1</sub>=Ax<sub>i</sub> iterations have completed. The programs should print on stdout when this parameter is set to 1. This will be used to test if your matrix-vector product is correct.</li>

 <li>You have sample input files at o <a href="http://www.cs.bilkent.edu.tr/~ozturk/cs426/fidapm08.mtx">http://www.cs.bilkent.edu.tr/~ozturk/cs426/fidapm08.mtx</a> o <a href="http://www.cs.bilkent.edu.tr/~ozturk/cs426/fidapm11.mtx">http://www.cs.bilkent.edu.tr/~ozturk/cs426/fidapm11.mtx</a> o <a href="http://www.cs.bilkent.edu.tr/~ozturk/cs426/cavity02.mtx">http://www.cs.bilkent.edu.tr/~ozturk/cs426/cavity02.mtx</a></li>

 <li>These test matrices will contain the sparse matrix in the following format – #rows #columns #non-zero-entries-in-A row column non-zero-value-at-A[row][column] row column non-zero-value-at-A[row][column]</li>

</ul>

.

.

(Till the end of file)

These sample files should be treated as normal text files.

<strong>Important</strong>: The rows and column numbers range start at 1 and therefore you must subtract 1 so that they start at 0 to match C style.  These matrices come from the “Matrix Market” website (<a href="http://math.nist.gov/MatrixMarket/">http://math.nist.gov/MatrixMarket/</a><a href="http://math.nist.gov/MatrixMarket/">)</a> which is an interesting place to browse if you are (and even if you are not)  into sparse computations.

<h1>Report</h1>




Write a short report containing:

<ol>

 <li>Parallelization strategy used (You can use any parallelization strategy that scales up.)</li>

 <li>Three figures for each test matrix that contains

  <ol>

   <li>parallel running time,</li>

   <li>speedup, and</li>

   <li>efficiency of your CUDA</li>

  </ol></li>

 <li>Short discussion about the results.</li>

</ol>

Note that, a part of your grading criteria may be the performance of your parallel implementation. Therefore you should try to write the fastest running parallel program.








