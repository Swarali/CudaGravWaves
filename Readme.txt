
			------README-----

1.Octave : 
   a. chirpfr4.m :
	Plots the chirp signal with noise and its fourier transform
	and calculate the inner product (uses innerpr.m)

	Input values : starting frequency, size of signal(in sec), sampling rate, end frequency, template size(in sec)
	Run in octave : chirpfr4(10,5,200,50,3);


   b. chirpfr5.m :
	Plots two chirpsignals which just cross the inner product of 0.97 for a given changing rate (use innerpr.m)

	Input values :  starting frequency, size of signal(in sec), sampling rate, end frequency, minimum change in frequency
	Run in octave :  chirpfr5(10,5,500,100,0.001)

   c.innerpr.m : 
	function used by other files to calculate inner product

2.MatchedfilteringC :
   a. frplot2.c :
	Plots data, fourier transform and inverse transform of the fourier transform using gnuplot (uses plotdata.c and four1.c)
	
	Run:>gcc frplot2.c four1.c plotdata.c -lm
	   :>./a.out
	Test Input values : Frequency : 10

   b. four1.c
	computes fft and ifft of the given array

   c. plotdata.c :
	plots data from a file input using gnuplot

3.GPU ://TODO - Add cpu_measure.c and gpu_measure.cu, Add/Change compile and run options of all the files
   a. reportcode1.c :
	Calculates correlation for the given frequency, number of samples, sampling frequency and time period (uses four1.c)
	Note : sampling frequency * timeperiod must be power of 2

	Run :> gcc reportcode1.c four1.c -lm
	     > ./a.out
	Test Input values : Sampling frequency : 32, Time period : 8, Number of Samples : 250, Frequency : 100

   b. reportcode2.cu :
	Calculates correlation on GPU using cudafft library using signal function from ContinuousGrav/wave[Running on windows]
	Note : sampling frequency * timeperiod must be power of 2

	Run:>nvcc reportcode2.cu -lcufft
	    >./a.out
	Test Input values : Sampling frequency : 32, Time period : 8, Number of Samples : 250, Frequency : 100

4.ContinuousGrav :
   a. wave.c
	Generates continuous gravitational wave signal from the input frequency and time period

	Run :>gcc wave.c four1.c -lm
	     >./a.out
	Test Input values : Frequency : 10, Time period : 86400


5.SOP	://TODO - Add compile and run options along with test input
	a.cpu_measure.c
		Measures the time taken for correlation on CPU
		Calulates correlation coefficient serial code by taking the inner product of fourier tranform
		-Uses the cor_host function from GPU/reportcode.c for doing correlation

	b.four1.c
		For computing FFT
		-with minor changes from MatchedfilteringC/four1.c to improve efficiency
	
	c.signal.c
		Signal function - generates gravitational wave signal
		
	d.gpu_measure.cu
		Measures the time taken for correlation on CPU
		Calculates correlation coefficient GPU code by using CUBLAS library function - cublasSgemv : which takes matrix and vector product
		
	
		