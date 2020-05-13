# Scoring

This section describes how the docking poses were scored. Whilst docking does generate binding scores, these are
widely known not to correlate well with binding affinities, especially for fragments, so two additional tools developed at
Oxford University were used to generate additional predicted binding scores.

## Live Resources

| usegalaxy.eu | 
|:--------:|
| <FlatShield label="history" message="view" href="https://usegalaxy.eu/u/timdudgeon/h/mpro-x0161" alt="Galaxy history" /> | 
| <FlatShield label="workflow" message="run" href="https://usegalaxy.eu/u/sbray/w/mpro-transfs-scoring" alt="Galaxy workflow" />  <FlatShield label="workflow" message="run" href="https://usegalaxy.eu/u/sbray/w/mpro-sucos-scoring" alt="Galaxy workflow" /> | 


## Outline

- The 25 docked poses for each enumerated charge state of the candidate compounds were scored using [TransFS](https://usegalaxy.eu/root?tool_id=xchem_pose_scoring) [1]. This step
is executed in a Docker container and requires a GPU for execution. Scores range from 0 (bad) to 1 (good). The score is
recorded as the `TransFSScore` property in the resulting SD file.
- Those scored poses are sorted and filtered so that only the top TransFS scoring pose for each original candidate (before
charge enumeration) is retained.
- Those top poses are then scored with the [SuCOS Max](https://usegalaxy.eu/root?tool_id=toolshed.g2.bx.psu.edu/repos/bgruening/sucos_max_score/sucos_max_score) [2] tool to generate a score that reflects the charge and feature overlap with the original 17 fragment ligands. Bigger scores are better and indicate more overlap.

The resulting poses have scores from rDock for docking as well as for [TransFS](https://usegalaxy.eu/root?tool_id=xchem_pose_scoring) and [SuCOS](https://usegalaxy.eu/root?tool_id=toolshed.g2.bx.psu.edu/repos/bgruening/sucos_max_score/sucos_max_score).

## Histories and workflows

A Galaxy workspace (history) containing the most current analysis can be imported from [here](https://usegalaxy.eu/u/timdudgeon/h/mpro-x0161).

The publicly accessible [TransFS scoring workflow](https://usegalaxy.eu/u/sbray/w/mpro-transfs-scoring) and [SuCOS scoring workflow](https://usegalaxy.eu/u/sbray/w/mpro-sucos-scoring) can be downloaded and installed on any Galaxy instance. They contain version information for all tools used in this analysis.

| Scoring workfows  |
|:----------------:|
|![](./w-transFS-scoring.png) |
| TransFS scoring workflow <FlatShield label="workflow" message="run" href="https://usegalaxy.eu/u/sbray/w/mpro-transfs-scoring" alt="Galaxy workflow" /> |
|![](./w-SuCOS-scoring.png)|
| SuCOS scoring workflow <FlatShield label="workflow" message="run" href="https://usegalaxy.eu/u/sbray/w/mpro-sucos-scoring" alt="Galaxy workflow" /> |




## References

[1] TransFS -Scantlebury et al., Dataset Augmentation Allows Deep Learning-Based Virtual Screening To Better Generalise To Unseen Target Classes, And Highlight Important Binding Interactions. URL: https://www.biorxiv.org/content/10.1101/2020.03.06.979625v1 

[2] SuCOS - Leung et al., SuCOS is Better than RMSD for Evaluating Fragment Elaboration and Docking Poses, [doi:10.26434/chemrxiv.8100203.v1](https://chemrxiv.org/articles/SuCOS_is_Better_than_RMSD_for_Evaluating_Fragment_Elaboration_and_Docking_Poses/8100203/1)
