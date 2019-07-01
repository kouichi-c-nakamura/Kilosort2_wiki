This page will keep track of the major modifications to the pipeline.

**v0.3 (February 2019): first public release; includes more automation.**
1. Removed a number of optimization steps that were judged ineffective. The spike amplitude variance is no longer empirically calculated, and is instead fixed and incorporated into the ops.lam parameter the way it is in Kilosort1. One of the two types of merging during the optimization was removed, because it was never used.
2. Default ops.lam value changed to 10, due to the above. The ops.lam parameter is now equivalent to the corresponding parameter in Kilosort1.
3. Several of the variables that accumulate during optimization (dWU, W, nsp) were switched from singles to doubles to lower the run-to-run variability. Some variability still exists, which we believe is due to numerical errors from using single variables on the GPU. This is unavoidable, since most GPUs have much faster processing of single-typed data, but should have minimal impact on the final results.  
4. A new merging step was added at the end of the optimization. It is similar to the merges during optimization, in that waveforms that are correlated get merged. Unlike the main optimization, no restriction is put on the amplitudes of the waveforms to be merged, so that a unit with high amplitude variability can be consolidated. However, this step also requires that the cross-correlogram (CCG) should have a very clear refractory period.  
5. A bug was fixed in the splitting step, where the spikes were not re-ordered according to drift before high-pass filtering. This resulted in much less effective splits.
6. As a consequence of 5, the ccsplit threshold (now called AUCsplit) can now be lowered significantly before too many false positives are found. The default changes to 0.9.
7. A veto step was added to the splits: if a split would result in a refractory CCG, it is not performed.
8. Units with clean auto-correlograms (few refractory violations) are labelled as good, in rez.good, and in Phy. The default threshold is 20% estimated contamination.
9. A step was added before data preprocessing where bad channels (no spikes) are detected and removed.
10. The Kilosort GUI was updated. The data views now use the actual time-varying templates tracked by Kilosort2. The adjustable parameters were restricted to Th, AUCsplit and lam. The GUI now allows the creation of new probe geometries. A wiki was added to guide the GUI user.
11. A new batch re-ordering algorithm was added (rastermap), to be tried if the default fails in some noticeable way.

**v0.2 (June 2018): first fully functional version, which fuses drift tracking with template matching.**
1. Used in original Stringer, Pachitariu et al, 2018b preprint.
2. Ongoing testing by collaborators.

**v0.1 (April 2018): initial batch re-ordering algorithm and drift correction.**
1. This original version did not contain template matching, and the spikes were instead detected by threshold crossing.
2. Used in original Stringer, Pachitariu et al, 2018a preprint.
