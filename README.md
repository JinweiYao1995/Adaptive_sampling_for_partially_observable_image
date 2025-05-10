# Adaptive_sampling_for_partially_observable_image

To replicate the simulation results, one just needs to run the `Intergrate.R` file. We primarily utilize the `MASS` and `RSpectra` packages, along with the `source` function, to access the other R files.

## Interpret the Result

The output of the simulation is based on Setting I out-control pattern. The output from `Model1_simulation.R` corresponds to Fig. 1(a), and `Model2_simulation.R` corresponds to Fig. 1(b). These outputs are combined in `Intergrate.R` to complete Fig. 1 in the manuscript.

The output will consist of 3 subplots in a single column, corresponding to the available sub-images r = 10, 7, 4 out of a total of p = 25 sub-images. Each subplot will contain four lines representing:
- Proposed MFPCA with Δ = 0.01
- FPCA with Δ = 0.01
- FPCA RS method
- MFPCA fully observed method

The x-axis shows the mean-shift magnitude, and the y-axis shows the corresponding ARL results.

Tables A1 and A2 in the appendix study the ARL₁ results and their standard errors under different choices of Δ = 0.01, 0.05, 0.1. These results are stored in the variables `output1` and `output2`, where ARL₁ values are in odd-numbered rows and standard errors in even-numbered rows. ARL₁ and standard error results for the MFPCA fully observed method are also included in these tables and are stored in `full1` and `full2`.

The simulation uses 500 repetitions for computing ARL, taking about 12 hours per model (approximately 25 hours total). This time is due to processing roughly 500×500 image samples. You can scale this down—for instance, 100 repetitions will take about 5 hours.

To change the number of ARL repetitions, modify:
- Lines 122–142 in `Model1_simulation.R`
- Lines 120–140 in `Model2_simulation.R`

Edit the loop variable `i` and the size of the array `oc_run`.

## Modify the Simulation

You can switch between Setting I and Setting II by editing:
- Lines 75–85 in `Model1_simulation.R`
- Lines 70–80 in `Model2_simulation.R`

## File Structure and Function Summary

The demo folder contains the following 8 files:

1. **top_fpca.R**: Methods for ARL₁ using FPCA with Δ = 0.01, 0.05, 0.1  
   Functions:
   - `ARLi_init`: helper to initiate CUSUM chart  
   - `Get_ARLi`: get running length  
   - `cusum_fpca`: sample redistribution under top-q framework  

2. **top_arl.R**: Methods for ARL₁ using MFPCA with Δ = 0.01, 0.05, 0.1  
   Functions:
   - `ARL_initial`: helper to initiate CUSUM chart  
   - `Get_ARL`: get running length  
   - `cusum_stage`: sample redistribution under top-q framework  

3. **top_rs.R**: Methods for ARL₁ using random sampling (RS) method  
   Functions:
   - `RS_initial`: helper to initiate CUSUM chart  
   - `RS_ARL`: get running length  
   - `cusum_RS`: sample redistribution under top-q framework  

4. **mfpca_estimation.R**  
   - `mfpca_est`: estimate MFPCA parameters using training samples  
   - `mpfca_score`: convert image samples into MFPCA scores  

5. **fpca_est.R**  
   - `fpca_est`: estimate FPCA parameters using training samples  
   - `fpca_score`: convert image samples into FPCA scores  

6. **Guess_L.R**  
   Implements binary search to find control limits `h` (related to Appendix Section C).  
   **Note**: To approximate control limits, use the correct data generation model and estimate FPCA/MFPCA parameters. For demonstration, precomputed limits are provided. You can verify by setting the mean-shift magnitude to 0 and checking ARL₀ results.

7. **Model1_simulation.R**  
   Functions to generate in-control and out-of-control data for Model I:
   - `Gen_X()`: in-control samples  
   - `Gen_OC()`: out-of-control samples with Setting I pattern  

8. **Model2_simulation.R**  
   Functions to generate in-control and out-of-control data for Model II:
   - `Gen_X()`: in-control samples  
   - `Gen_OC()`: out-of-control samples with Setting I pattern  

## Reference

The detailed implementation can be found in the following paper:  
https://www.tandfonline.com/doi/abs/10.1080/00224065.2023.2282512

## Citation

If you find this work useful, please consider citing:

```bibtex
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

