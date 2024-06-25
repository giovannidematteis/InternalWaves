# InternalWaves
Collection of codes used for results of Nature Communication submission "Interacting internal waves explain global patterns of interior ocean mixing"

This repository contains the main codes used to obtain the results in the manuscript for transparency about reproducibility of the results. However, the values of the parameters currently set in the codes may not correspond to the values used to obtain the results in the paper.
If in doubt about the meaning of parts of the code, please reach out to the corresponding author at giovannidematteis@gmail.com


This repository contains a 6-step processing organized as follows:

- Folder 'superscripts'.
  
Instructions -> run the code 'superscript.m' (run time about 2-3 weeks);

performs the theoretical calculations computing all the fluxes between all points in Fourier space;

output is 25 files 'NDOTS-...' (high freq part) and 25 files 'NDOTS-...-lf' (low frequency part)
corresponding to the 25 spectra in the space inertial slope (s, or s_NI) - continuum slope (y, or s_omega)
that we use in our spectral representation to derive the fluxes for any spectral slopes, by interpolation;

- Folder 'process_fluxes'.

Instructions -> run the code 'process_ndot_lf.m' for each of the 'NDOTS-...' pair of files; versions 'signed' and 'named' are used to split the contributions by interaction type; run the codes 'plot_fluxes...' for representing spectral energy transfers as arrows between boxes

input: the 50 files 'NDOTS-...';

output: 25 files 'F_...' for the 25 spectra in the s-y space (save manually or add line at the end).

- Folder 'process_spectrum'.

Instructions -> run the code 'parameterization_grid.m'; latest update 'parameterization_grid_3D.m' also includes m slope 

input: the 25 files 'F_...'

output: matrix 'Fs' saved in matlab workspace (needed for next steps)

- Folder 'compute_GMACMD_series'.

Instructions -> run the code 'compute_slopes_all.m', or 'compute_timescales.m';

computes the inertial slope s (s_NI) and the continuum slope y (s_omega) and the theoretical
dissipation rate for each observational spectrum

input: all of the approximately 3000 .mat files processed by Arnaud Le Boyer [1] containing the daily spectra
for the GMACMD timeseries; Fs matrix in matlab workspace (computed at previous step) needed to calculate the
dissipation for each observational spectrum;

output: structure 'Statistics_NIstretched.mat' file, with slopes, coordinates, dissipation for
each daily spectrum from GMACMD.

- Folder 'mooring_bins'.

Instructions -> run the code 'mooring-bins.m';

Performs an average (saving also the standard deviation)
of all the mooring dissipations that fall inside a certain geographical partition in
bins for which a mean estimate of dissipation is also available from strain estimates from ARGO obtained by Friederike Pollmann [2];

input: file 'Statistics_NIstretched_Gio.mat' (this file is not in this repository for size constraints);

output: structure 'mooring_Stat.mat' with all the stats from moorings related to all bins

- Folder 'strain_based'.

Instructions -> run the 3 codes 'global_strain...' in order;

performs the processing and regional comparison (bin by bin) of our dissipation from the GMACMD series
and the corresponding average dissipation in Caitlin Whalen's analysis

input: 3 files 'av_world_e_...' provided by Caitlin Whalen; our structure 'mooring_Stat.mat'

output: direct comparison, all sorts of figures to observe the patterns in the comparison

Latest update: 'global_strain_Pollmann' uses Friederike Pollmann's Argo estimates from 2023 [3].


References to databases:

[1] The GMACMD database is not contained in this repository - only one exemplary file 'acc08518_SI.mat' in the folder 'compute_GMACMD_series'. Please contact aleboyer@ucsd.edu

[2] https://doi.org/10.5281/zenodo.6966416

[3] Please download those estimates from the online repository provided as reference in the manuscript: https://doi.org/10.17882/95327.

Disclaimer:
Please treat this repository with care and reach out to giovannidematteis@gmail.com for doubts on the various pieces of code and their mutual interplay. Please keep in mind that this is a collection of the base codes that were developed to obtain our results, made publicly available for transparency. At the current stage, this is not meant to serve as a user-friendly platform.
