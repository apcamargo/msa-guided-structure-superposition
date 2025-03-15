# msa-guided-structure-superposition

Aligns a set of PDB files based on residue correspondence derived from a multiple sequence alignment (MSA) provided in FASTA format. The method extracts alignment information from the MSA to guide structural superposition, minimizing the root-mean-square deviation (RMSD) between the aligned structures.

## Example usage

Starting with a directory containing PDB files (named `structures` in this example), an MSA must first be generated. This can be done using sequence-based tools (e.g., [MUSCLE](https://github.com/rcedgar/muscle/) or [MAFFT](https://mafft.cbrc.jp/alignment/software/)), or structure-based tools (e.g., [MUSCLE-3D](https://github.com/rcedgar/muscle/) and [FoldMason](https://github.com/steineggerlab/foldmason)).

In this example, MUSCLE-3D is used:

```sh
reseek -pdb2mega structures -output structures.mega
muscle -align structures.mega -output msa.afa
```

Next, run `msa-guided-structure-superposition` to align the structures:

```sh
pixi run msa-guided-structure-superposition msa.afa structures/* -o aligned_structures
```

`msa-guided-structure-superposition` first identifies the MSA columns shared by all sequences. It then selects a reference structure and aligns each additional structure to it using these common columns. The rotated structures are saved in the `aligned_structures` directory.
