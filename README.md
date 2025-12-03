# rna-toys / quizzes / playground / tutorials

<p align="center" style="font-size:20px">
  <img style="height:200px;" src="https://github.com/user-attachments/assets/bb8c5931-b417-411a-a864-06eb8f8085ba">
</p>

> [!NOTE]
> (hmm... it's more like quizzes, because I'm not giving excellent explanations ;-) So maybe it's not tutorials ;-))

rna-tutorials is a hands-on repository with shell scripts and command examples demonstrating practical RNA analysis workflows and basic Infernal/RNA-tools usage, aimed at education and reproducible tutorials.

1. Make a sequence alignments of two RNA sequences (`infernal-align-two-seqs-to-rfam-model`), the two tRNA molecules share an almost identical 3D fold despite only 63% sequence identity in their aligned regions #infernal #rfam
1. Calculate RMSD between two structures of homologs? (`rna-3d-rmsd-for-tRNAs`) - 3D structural alignment between two tRNA molecules #pymol #infernal #rfam
1. Secondary structure, returns matrix of interactions[^1] (`secondary-structure-interaction-arrays`) #python #numpy
1. Get secondary structure for tRNA (1ehz) #rnatools
     - using frabase (https://rnafrabase.cs.put.poznan.pl)
1. Annotate secondary strucure for `tetraloop_steamOf1bp.pdb` (with rna-tools.online) #rnatools
1. Detect covariation from an RNA alignments and annotate RNA Secondary Structures (RNAView)[^2] with R-scape (`secondary-structure-covariation-and-annotation-with-rscape`)[^3]

## AlphaFold2
  
1. Structural Module of MiniRoseTTA https://github.com/mmagnus/StructuralModuleOfMiniRoseTTA

## AlphaFold3

#TODO diffusion
 
## RNA Edit

  #TODO add extract with rna-tools
  
## Tips

- see all tRNA structures - https://rfam.org/family/RF00005#tabview=tab6 

## Tools

### rna-tools

https://rna-tools.readthedocs.io/

rna-tools: a toolbox to analyze structures and simulations of RNA

    RNA-Puzzles toolkit: A computational resource of RNA 3D structure benchmark datasets, structure manipulation, and evaluation tools.
    M. Magnus, M. Antczak, P. Lukasiak, J. Wiedemann, T. Zok, J. M. Bujnicki, E. Westhof, M. Szachniuk, and Z. Miao
    Nucleic Acid Research, vol. 48, no. 2, pp. 576–588, Jan. 2020

`rna-tools in colab` https://colab.research.google.com/drive/1PsnQRAKbIhKGuxmhiZ5fSeBkjfQRieSS?usp=sharing
 
<p align="center">
  <img src="https://github.com/user-attachments/assets/d36b2129-12ec-466d-b191-3d00fcb51dbd"
       alt="rna-tools"
       width="500">
</p>

### rna-tools.online

https://rna-tools.online

rna-tools.online is an online gateway to some of the rna-tools functionalities

    rna-tools.online – a Swiss army knife for RNA 3D modeling workflows  
    M. Magnus  
    Nucleic Acid Research, 10.1093/nar/gkac372, May 2022  

### emacs-pdb-mode

<img width="463" alt="emacs-rna-tools" src="https://github.com/user-attachments/assets/fcb92417-06f0-44d9-813a-7fa38251e73d" />

Emacs for editing files in the PDB format https://github.com/mmagnus/emacs-pdb-mode

## Examplary inputs

    >1ehz (tRNA)
    GCGGAUUUAGCUCAGUUGGGAGAGCGCCAGACUGAAGAUCUGGAGGUCCUGUGUUCGAUCCACAGAAUUCGCACCA
    (((((((..((((.....[..)))).((((.........)))).....(((((..]....)))))))))))).... 
    GCGGAUUUAGCUCAGUuGGGAGAGCGCCAGACUGAAGAUCUGGAGGuCCUGUGUUCGAUCCACAGAAUUCGCACCA #fasr from_stockholm
    (((((((..((((........)))).(((((.......))))).....(((((.......)))))))))))).... #fasr from_stockholm

    # ss from https://rnafrabase.cs.put.poznan.pl/?act=pdbdetails&id=1EHZ

https://www.rcsb.org/structure/1EHZ

[^1]: https://rna-tools.readthedocs.io/en/latest/_modules/rna_tools/SecondaryStructure.html#parse_vienna_to_pairs

[^2]: https://github.com/rcsb/RNAView

[^3]: http://rivaslab.org/software.html
