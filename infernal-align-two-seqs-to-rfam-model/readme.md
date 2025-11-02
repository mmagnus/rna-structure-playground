# Aligning Two tRNA Sequences to an Rfam Model (RF00005)

To align two homologous tRNA sequences—1ehz and 6Y2L_2—to the RF00005.cm covariance model (tRNA family) from Rfam, using Infernal’s cmalign toolg.

This process maps both input sequences onto the consensus secondary structure and reference alignment defined by the Rfam model.

Input Files

combo.fa — combined file used for alignment:

	>6Y2L_2|Chain B[auth B4]|tRNA|Homo sapiens (9606)
	GCCCGGAUAGCUCAGUCGGUAGAGCAGGGGAUUGAAAAUCCCCGUGUCCUUGGUUCGAUUCCGAGUCCGGGCACCA
	>1ehz
	GCGGAUUUAGCUCAGUUGGGAGAGCGCCAGACUGAAGAUCUGGAGGUCCUGUGUUCGAUCCACAGAAUUCGCACCA

Aligned two tRNA sequences (human 6Y2L_2 and E. coli 1ehz) to the Rfam tRNA model, producing a Stockholm alignment showing conserved secondary structure and strong sequence similarity across canonical tRNA stems and loops.	

	$ cmalign RF00005.cm combo.fa

	# STOCKHOLM 1.0
	#=GF AU Infernal 1.1.5

	#=GS 6Y2L_2|Chain DE B[auth B4]|tRNA|Homo sapiens (9606)

	6Y2L_2|Chain         GCCCGGAUAGCUCAGUcGGUAGAGCAGGGGAUUGAAAAUCCCCGUGuCCUUGGUUCGAUUCCGAGUCCGGGCAcca
	#=GR 6Y2L_2|Chain PP ***********************************************************************84444
	1ehz                 GCGGAUUUAGCUCAGUuGGGAGAGCGCCAGACUGAAGAUCUGGAGGuCCUGUGUUCGAUCCACAGAAUUCGCAcca
	#=GR 1ehz         PP ****************9555***************************************************84444
	#=GC SS_cons         (((((((,,<<<<___.____>>>>,<<<<<_______>>>>>,,,.,<<<<<_______>>>>>))))))):...
	#=GC RF              GgagauaUAGCucAgU.GGUAgaGCgucgGaCUuaaAAuCcgaagg.cgcgGGUUCgAaUCCcgcuaucucCa...

this time save an alignmets as `combo.sto` in about 0.03 s.

	$ cmalign -o combo.sto RF00005.cm combo.fa
	
	# cmalign :: align sequences to a CM
	# INFERNAL 1.1.5 (Sep 2023)
	# Copyright (C) 2023 Howard Hughes Medical Institute.
	# Freely distributed under the BSD open source license.
	# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
	# CM file:                                     RF00005.cm
	# sequence file:                               combo.fa
	# CM name:                                     tRNA
	# saving alignment to file:                    combo.sto
	# number of worker threads:                    4
	# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
	#                                                                              running time (s)
	#                                                                       -------------------------------
	# idx  seq name      length  cm from    cm to  trunc    bit sc  avg pp  band calc  alignment      total  mem (Mb)
	# ---  ------------  ------  -------  -------  -----  --------  ------  ---------  ---------  ---------  --------
		1  6Y2L_2|Chain      76        1       71     no     40.92   0.966       0.00       0.02       0.02      1.36
		2  1ehz              76        1       71     no     39.49   0.947       0.00       0.02       0.02      1.58
	#
	# CPU time: 0.03u 0.00s 00:00:00.03 Elapsed: 00:00:00.03

Get sequence identity:

	$ esl-alistat combo.sto

	//
	Alignment number:    1
	Format:              Stockholm
	Number of sequences: 2
	Alignment length:    76
	Total # residues:    152
	Smallest:            76
	Largest:             76
	Average length:      76.0
	Average identity:    63%
	//
	Compilation finished

esl-alistat combo.sto confirmed that the alignment produced by cmalign contained two 76-nt sequences with 63% average identity, stored in a single 76-column Stockholm alignment.

The result is a Stockholm alignment showing both sequences aligned to the Rfam model. It includes consensus structure and per-position annotation lines.

Practical Takeaway

The alignment confirms that both 1ehz (E. coli tRNA-Phe) and 6Y2L_2 (human tRNA) share conserved tRNA structural motifs (acceptor stem, D-loop, anticodon stem-loop, TΨC loop), validating cross-species structural conservation captured by the Rfam tRNA covariance model RF00005.

