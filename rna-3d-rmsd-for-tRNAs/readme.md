# 3D structural alignment between two tRNA molecules

This PyMOL session shows a 3D structural alignment between two tRNA molecules — the yeast phenylalanine tRNA (1ehz) and the human ribosomal tRNA fragment (6y2l_B4) — to evaluate their spatial similarity.

This PyMOL run demonstrates that human and yeast tRNAs maintain nearly identical 3D geometry (RMSD ≈ 4.9 Å*) even though their sequences share only 63% identity, underscoring the strong evolutionary conservation of the tRNA fold.

 * However, you can also see that PyMOL fails to properly align sequences containing modified nucleotides, so many residues remain unmatched or stripped during the alignment.

-------------------------------------------------------------------------------


![](img
.png)

	PyMOL>fetch 6y2l_B4
	TITLE     Structure of human ribosome in POST state
	 ExecutiveLoad-Detail: Detected mmCIF
	 CmdLoad: "./6y2l.cif" loaded as "6y2l_B4".
	PyMOL>fetch 1ehz
	TITLE     The crystal structure of yeast phenylalanine tRNA at 1.93 A resolution
	 ExecutiveLoad-Detail: Detected mmCIF
	 CmdLoad: "./1ehz.cif" loaded as "1ehz".
	PyMOL>aa

		RaR  RMSD after refinement
		#AA  Number of aligned atoms after refinement
		CoR  Number of refinement cycles
		RbR  RMSD before refinement
		#AbR Number of aligned atoms before refinement
		RS   Raw alignment score
		AR   Number of residues aligned 

	Ref                  Model                RaR  #AA  CoR  RbR  #AbR RS   AR
	6y2l_B4              1ehz                 4.86 1147 5    7.23 1380 372  67  
	 parser: no matching selection.
	PyMOL>align 6y2l_B4, 1ehz, object='aln'
	 Match: read scoring matrix.
	 Match: assigning 77 x 245 pairwise scores.
	 MatchAlign: aligning residues (77 vs 245)...
	 MatchAlign: score 372.000
	 ExecutiveAlign: 1380 atoms aligned.
	 ExecutiveRMS: 61 atoms rejected during cycle 1 (RMSD=7.23).
	 ExecutiveRMS: 65 atoms rejected during cycle 2 (RMSD=6.49).
	 ExecutiveRMS: 45 atoms rejected during cycle 3 (RMSD=5.78).
	 ExecutiveRMS: 33 atoms rejected during cycle 4 (RMSD=5.34).
	 ExecutiveRMS: 29 atoms rejected during cycle 5 (RMSD=5.08).
	 Executive: RMSD =    4.865 (1147 to 1147 atoms)
	 Warning: Invalid characters in 'aln' have been replaced or stripped
	 Executive: object "aln" created.
	PyMOL>save trna.pse
	 Save: Please wait -- writing session file...
	 Save: wrote "trna.pse".
	PyMOL>sav trna.pse
	/opt/homebrew/bin/convert /var/folders/zj/bt4mkdcx7kb4j6scj6p82zw40000gq/T/tmp80rsr_l9.png -gravity center -crop 3:3 +repage /var/folders/zj/bt4mkdcx7kb4j6scj6p82zw40000gq/T/tmp9ei_hhn2.png
	/opt/homebrew/bin/fileicon set ~/Desktop/trna.pse.pse /var/folders/zj/bt4mkdcx7kb4j6scj6p82zw40000gq/T/tmp9ei_hhn2.png
