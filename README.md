Download Link: https://assignmentchef.com/product/solved-coen146l-lab-2-multithreading-in-c-and-file-transfer
<br>
<h5><strong>Multithreading in C – Copying files</strong></h5>

Problem: Write a C program to copy binary/ text files simultaneously.




Analysis:

<ul>

 <li>Input: pass file names as arguments to main(), so your main function needs to be defined as follows:</li>

</ul>

int main(int argc, char * argv[])

Your files: src.dat and dest.dat files.




<ul>

 <li>File reading can be accomplished by using either:

  <ul>

   <li>Functions: fopen, fwrite, and fread for binary files or fprintf and fscanf for text files

    <ul>

     <li>FILE *fopen(const char *filename, const char *mode)</li>

     <li>fwrite( ptr, int size, int n, FILE *fp ); or fprintf() (for text files)</li>

     <li>fread( ptr, int size, int n, FILE *fp ); or fscanf()  (for text files)</li>

     <li>fclose(ptr);</li>

    </ul></li>

  </ul></li>

</ul>

e.g.

FILE *fp;

fp = fopen(“src.dat”,”r”);

fp = fopen(“dest.dat”,”w”);

fwrite(&amp;buf,sizeof(buf),1,fp);

fread(&amp;buf,sizeof(buf),1,fp);

fclose(fp);







OR




<ul>

 <li>System calls: open, read, write

  <ul>

   <li>int open (const char* Path, int flags [, int mode ]);</li>

   <li>size_t read (int fd, void* buf, size_t cnt);</li>

   <li>size_t write (int fd, void* buf, size_t cnt);</li>

  </ul></li>

</ul>

e.g.:

int fd = open(“foo.txt”, O_RDWR);

int nw = write(fd, buf, strlen(buf));

int nr = read(fd, buf, 40);

close (fd);




You need to include the following libraries:

<ul>

 <li>#include&lt;sys/types.h&gt;</li>

 <li>#include&lt;sys/stat.h&gt;</li>

 <li>#include &lt;fcntl.h&gt;</li>

</ul>




You may create files of random data with different sizes/ bytes. You may use “cat” and “head” commands ( i.e. $cat /dev/random | head -c &lt;bytecount&gt;). /dev/random are special files that serve as pseudorandom number generator. “cat” is used to display the content and “head” is used to display the specified number of lines. So the result of “cat” is sent to the upstream end of PIPE and “head” receives these results and redirects the content of the specified bytes to a file.




$cat /dev/random | head -c 100000 &gt; src1.dat à creates a file with 100KB

$cat /dev/random | head -c 1000000 &gt; src2.dat à creates a file with 1MB




Check the size of the files with the command “ls -la”




<ul>

 <li>Write your C program to copy files (binary and text) using functions, compile, debug, run, and test</li>

 <li>Write your C program to copy files (binary and text) using system calls, compile, debug, run, and test</li>

 <li>Calculate the time taken to copy files for both step 1 and 2. You may useclock()function (in h library). Call the clock function at the beginning and end of the code to measure the time, subtract the values, and then divide by CLOCKS_PER_SEC (the number of clock ticks per second) to get processor time. You may use the following code snippet:</li>

</ul>




#include &lt;time.h&gt;          clock_t start, end;     <strong>double</strong> cpu_time_used;          start = clock();     … /* Time consuming process. */     end = clock();     cpu_time_used = ((<strong>double</strong>) (end – start)) / CLOCKS_PER_SEC;




<ul>

 <li>Write your C program to copy multiple files (say 10 files) by creating threads, each of which will be responsible of copying one file. Use good style practices, compile, debug, run, and test for large sizes of matrices.</li>

</ul>


