# R10_8oxoG_Models
This repository contains two basecallers and two modification callers for 8oxoG detection. Models were created for the sole purpose of detecting 8oxoG in conserved mitochondria contexts across both mice and human genomes. Note, basecalling with compatible model is needed to be done before modification calling in order for model to work.

## Contexts 

Overall, two models were created. The SJ model looked at eight contexts within the mitochondrial genome, see below: TCAAAGTAACT, TAAAAGARTTA, ACTTTGATAGA, TGATAGAGTAA, TGTCTGATAAA, TCAACGATTAA, TTAAAGTCCTA, ACTCAGATCAC

The TTAGGG model looked at any TTAGGG context in the mouse or human mitochondria. See specific contexts attached in the file: TTAGGG_human_mouse_contexts.txt

DISCLAIMER: Use of models on other contexts than those listed above will result in erroneous results. Models were trained for specific contexts as this was found to result in the highest accuracy.

## Dorado Basecalling models 

Usage: Only use basecalling models if you are basecalling data with elevated levels of 8oxoG for the purpose of detecting 8oxoG.

dna_r10.4.1_e8.2_400bps_sup_@v4.2.0_OxoG_SJ - dorado basecalling model finetuned for calling 8oxoG as G in the eight single contexts above in the mitochondria. Note, model is finetuned from dorado model dna_r10.4.1_e8.2_400bps_sup_@v4.2.0.

dna_r10.4.1_e8.2_400bps_sup@v5.0.0_OxoG_TTAGGG - dorado basecalling model finetuned for calling 8oxoG as G in any TTAGGG context in the mitochondria. Note, model is finetuned from dorado model dna_r10.4.1_e8.2_400bps_sup@v5.0.0_OxoG. 

Example basecalling with model: dorado basecaller ${model_path} ${pod5_path} --reference ${reference_fa_file} --device "cuda:0" --recursive --emit-moves

## Remora Modification Caliing Models

SJ_mito_8oxoG.pt - model for calling 8oxoG in the eight single contexts above in the mitochondria

TTAGGG_mito_8oxoG.pt - model for calling 8oxoG in any TTAGGG contexts in the mitochondria

Example modification calling with model: remora infer from_pod5_and_bam ${pod5_path} ${bam_path} --model ${model_path} --out-bam ${out_bam_path} --num-extract-alignment-workers 24 --num-prepare-read-workers 24 --num-prepare-nn-input-workers 24 --num-post-process-workers 24 --device 0 --batch-size 1024

## Further information and thesis

If you would like any further information regarding the SJ model, then read the thesis:
Characterization of allele-specific 5-methylcytosine in cancer and quantification of 8-oxoguanine using nanopore sequencing - Andrew Galbraith UBC MSc Thesis
https://open.library.ubc.ca/soa/cIRcle/collections/ubctheses/24/items/1.0444093
