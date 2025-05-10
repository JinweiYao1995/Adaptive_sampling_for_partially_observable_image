# Adaptive_sampling_for_partially_observable_image

To replicate the simulation results, one just needs to run 'Intergrate.R” file. We primarily utilized the ‘MASS’ and ‘RSpectra’ packages, along with the ‘source’ function, to access the other R files. 

Interpret the result: 

The output of the simulation will be based on Setting I out-control pattern. The output from the 'Model1_simulation.R' correspond to fig.1(a) and 'Model2_simulation.R' correspond to fig.1(b) respectively. These outputs are combined in 'Intergrate.R’ to complete the fig.1 in the manuscript. The output will consist of 3 subplots in a single column, correspond ing to to the available sub-image r = 10,7,4 out of a total p = 25 sub-images. Each subplot will contain four lines representing the proposed MPFCA with Δ = 0.01 ,  FPCA with Δ = 0.01 methods and FPCA RS method, and finally, the MFPCA fully observed method, respectively. These line plots will show the mean-shift magnitude on the x-axis and corresponded ARL result on the y-axis.

The table A1 and A2 from the appendix study the ARL_1 results along with their standard errors, under difference choice of Δ = 0.01,0.05,0.1. These results are stored in variables “output1” and “output 2”. In these variables, ARL_1 information is found in every odd line, while the standard error is located in every even row. Furthermore, the ARL_1 and standard errors of the MFPCA fully observed method have been incorporated into Table A1 and A2 in the appendix. These augmented results can be located in the variables ‘full1’ and ‘full2’. 

In terms of the time consumption of this sample code, we  compute ARL results based on 500 repetitions, which takes 12 hours for each model I and model II (total 25 hours). The reason for the long time consumption is that is that we essentially process 500*500 images. The time consumption will change proportionally to number of repetition be selected. For example,  it will only take approximates 5 hours to finish the same simulation, if the ARL results is computed based on 100 repetitions. One can adjust the number of ARL repetition in lines 122-142 in file 'Model1_simulation.R' (lines 120-140 in file 'Model2_simulation.R’) by changing the iteration number of “i” and the size of the storing array ‘oc_run’. 

To replicate the other results in the paper, one can modify the simulation setting by going to “Model1_simulation.R” and “Model2_simulation.R”. The shift type can be switched between Setting I and Setting 2 by editing lines 75-85 in file 'Model1_simulation.R' and lines 70-80 in file 'Model2_simulation.R'. 

Detailed of files layout and functions are also contained. The demo folders have 8 other files: 

1. top fpca.R: include methods required for ARL_1 for FPCA Δ = 0.01,0.05,0.1
Which has following function: 
	ARLi_init: helper function for initiate CUSUM chart 
           Get_ARLi: Get running length under FPCA Δ
           cusum_fpca: helper function for sample redistribution top-q framework

2. top arl.R: include methods required for ARL_1 for MFPCA Δ = 0.01,0.05,0.1
Which has following function: 
	ARL_initial: helper function for initiate CUSUM chart 
           Get_ARL: Get running length
           cusum_stage: helper function for sample redistribution top-q framework

3. top rs .R: include methods required for ARL_1 for Random Sampling method 
Which has following function: 
	RS_initial: helper function for initiate CUSUM chart 
           RS_ARL: Get running length
           cusum_RS:helper function for sample redistribution top-q framework

4. mfpca_estimation.R: 
	mfpca_est: estimate MFPCA parameters with training samples 
           mpfca_score: convert image sample into MFPCA scores 

5. fpca_est.R: 
	fpca_est: estimate FPCA parameters with training samples 
           fpca_score: convert image sample into FPCA scores 	

6. Guess_L.R: implement binary search  to find control limits h, correspond to appendix Section C.

Note: To approximate the control limits, one should use the correspond data generation model and estimated the MFPCA/FPCA parameters before proceeding. For the purpose of demonstration, we directly provide these limits in the sample codes. These limits can be examined by setting the mean shift magnitude to be 0 and retrieving ARL_0 results.

7. Model1_simulation. R: include two functions to generate in-control and other control data 
	Gen_X(): generate in-control samples from Model I 
           Gen_OC(): generate out-control samples from Model I, and impose the out-control pattern of Setting I 

8. Model2_simulation. R: include two functions to generate in-control and other control data 
	Gen_X(): generate in-control samples from Model II
        Gen_OC(): generate out-control samples from Model II, and impose the out-control pattern of Setting I 


The detail implementation can be referrred to this paper: https://www.tandfonline.com/doi/abs/10.1080/00224065.2023.2282512 


If you find this work useful, please consider citing:

@article{yao2024adaptive,
  title={Adaptive sampling and monitoring of partially observed images},
  author={Yao, Jinwei and Balasubramaniam, Badrinath and Li, Beiwen and Kreiger, Eric L and Wang, Chao},
  journal={Journal of Quality Technology},
  volume={56},
  number={2},
  pages={157--173},
  year={2024},
  publisher={Taylor \& Francis}
}
