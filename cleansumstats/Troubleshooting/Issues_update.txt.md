# Issues_update.txt
This is a precursor to [[7.1 Troubleshooting uncleaned sumstats]]
Not to be considered current.


```
# Documented issues with the 19 - 98

## Rerunning some of the ones that had some sort of lock or permissions issue:

---
## 35
FIXED

---
## 33,92,54,52

Returned a "broken pipe" type error. See further down below.

---
## 98

N E X T F L O W  ~  version 21.12.1-edge
Launching `/cleansumstats/main.nf` [golden_babbage] - revision: ef09f3f0cb
No such file: /cleansumstats/outdir/pipeline_info/execution_trace.txt.4 -> /cleansumstats/outdir/pipeline_info/execution_trace.txt.5

---
## 96

N E X T F L O W  ~  version 21.12.1-edge
Launching `/cleansumstats/main.nf` [berserk_shockley] - revision: ef09f3f0cb
No such file: /cleansumstats/outdir/pipeline_info/execution_trace.txt.3


---
---
## 22, 23, 97, 38, 36, 48, 32, 76, 90, 89, 20, 21, 27, 24, 26, 25, 31, 30, 29, 28
FIXED!

---
---
Possibly fixed as of 01.03.22

## 67, 66, 65, 64, 61, 59, 63, 62, 60, 69, 78, 77, 75, 74, 73, 72, 71, 70, 68

Reading metadata files
Failed to read/validate metadata file /cleansumstats/input/MAGIC_GLYCEMIC_2021_FG_SAS.cleansumstats_meta: - $.stats_TotalN: number found, integer expected

## 45, 44, 43,
Reading metadata files
Failed to read/validate metadata file /cleansumstats/input/GIANT_HEIGHT_2018_UKB.cleansumstats_meta: - $.path_sumStats: does not match the regex pattern ^[a-zA-Z0-9][a-zA-Z0-9_.-]+\.gz$



---
---


---
## 85, 86
 Reading metadata files
Postprocess metadata
Failed to read/validate metadata file /cleansumstats/input/PGC_ASD_2017_WW.cleansumstats_meta: Column 'or' (from metadata field 'col_OR') did not exist in sumstat file header: [1, 729679, rs4951859, C, G, 1.03, 0.96, 1.10, .0288, .036, .4251, .19, .652, 15954, --+-+-++++++-+]

---
## 41, 40, 37 
Reading metadata files
Postprocess metadata
Failed to read/validate metadata file /cleansumstats/input/GAMEON_COLON_2015_CORECT.cleansumstats_meta: Column 'OR' (from metadata field 'col_OR') did not exist in sumstat file header: [markername,Rs_numbers,coordinate,Build,strand,nstudy,ncase,ncontrol,effect_allele,ref_allele,eaf,imp_type_mecc,imp_type_cfr1,imp_type_cfr2,imp_mecc,imp_cfr,beta,se,OR,L_CI,U_CI,pvalue]

DEPRECEATE THESE FILES

---
## 80, 81, 82, 83, 84

Reading metadata files
Failed to read/validate metadata file /cleansumstats/input/NORMENT_BRAINSTEMVOLUMES_2019_Whole.cleansumstats_meta: - $.col_CHR: null found, string expected

---


---
## 46, 34, 47

Reading metadata files
Failed to read/validate metadata file /cleansumstats/input/ICBP_DBP_2011.cleansumstats_meta: - $.col_EffectAllele: is missing but it is required

DEPRECEATE THESE FILES



---









---
---

# The error output of the next 15 files are similar but the defining feature of the errors is unclear to me.
# See the one immediately below for a good example.

---
## 93,33

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_pgc_mdd_meta_no23andMe_noUKBB.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_pgc_mdd_meta_no23andMe_noUKBB.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_pgc_mdd_meta_no23andMe_noUKBB.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/ea/3c25a7301cb19fb28f7e10fbed70e2

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`


---

Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_PGC_SCZ_w3_90_0418b.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_PGC_SCZ_w3_90_0418b.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_PGC_SCZ_w3_90_0418b.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/35/c49a54ec5d1ca5545a7da98e866c3e

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line



executor >  local (4)
[29/4941d6] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[f6/d59632] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[29/82b1a8] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[35/c49a54] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_PGC_SCZ_w3_90_0418b.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_PGC_SCZ_w3_90_0418b.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_PGC_SCZ_w3_90_0418b.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/35/c49a54ec5d1ca5545a7da98e866c3e

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line



executor >  local (4)
[29/4941d6] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[f6/d59632] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[29/82b1a8] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[35/c49a54] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_PGC_SCZ_w3_90_0418b.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_PGC_SCZ_w3_90_0418b.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_PGC_SCZ_w3_90_0418b.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/35/c49a54ec5d1ca5545a7da98e866c3e

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line


---

Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_PGC_SCZ_w3_no_w2_41_0818a.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_PGC_SCZ_w3_no_w2_41_0818a.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_PGC_SCZ_w3_no_w2_41_0818a.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/af/17b51146c2500d9376f7f7cc0290cd

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`



executor >  local (4)
[2a/8b41da] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[83/ab0a2e] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[1c/5043b3] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[af/17b511] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_PGC_SCZ_w3_no_w2_41_0818a.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_PGC_SCZ_w3_no_w2_41_0818a.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_PGC_SCZ_w3_no_w2_41_0818a.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/af/17b51146c2500d9376f7f7cc0290cd

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`



executor >  local (4)
[2a/8b41da] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[83/ab0a2e] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[1c/5043b3] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[af/17b511] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_PGC_SCZ_w3_no_w2_41_0818a.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_PGC_SCZ_w3_no_w2_41_0818a.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_PGC_SCZ_w3_no_w2_41_0818a.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/af/17b51146c2500d9376f7f7cc0290cd

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`


---
## 42

executor >  local (4)
[56/fdb258] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[9e/9d5cd3] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[eb/086ef9] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[19/78b99d] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat combined_overall04022014.assoc.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh combined_overall04022014.assoc.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat combined_overall04022014.assoc.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/19/78b99d6358d26bf24139b5fdd68573

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line



executor >  local (4)
[56/fdb258] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[9e/9d5cd3] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[eb/086ef9] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[19/78b99d] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat combined_overall04022014.assoc.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh combined_overall04022014.assoc.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat combined_overall04022014.assoc.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/19/78b99d6358d26bf24139b5fdd68573

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line



executor >  local (4)
[56/fdb258] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[9e/9d5cd3] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[eb/086ef9] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[19/78b99d] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat combined_overall04022014.assoc.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh combined_overall04022014.assoc.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat combined_overall04022014.assoc.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/19/78b99d6358d26bf24139b5fdd68573

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line


WARN: Can't read history file: .nextflow/history

---
## 39


executor >  local (2)
[bd/f2a4a0] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[-        ] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[-        ] process > make_metafile_unix_friendly    [  0%] 0 of 1
[3e/dbb627] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat Psoriasis.meta.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh Psoriasis.meta.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat Psoriasis.meta.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  tr: write error: Broken pipe
  .command.run: line 23: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/3e/dbb627e640084f13e8799a32b4329b

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line



executor >  local (3)
[bd/f2a4a0] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[62/de9b68] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[-        ] process > make_metafile_unix_friendly    [  0%] 0 of 1
[3e/dbb627] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat Psoriasis.meta.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh Psoriasis.meta.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat Psoriasis.meta.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  tr: write error: Broken pipe
  .command.run: line 23: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/3e/dbb627e640084f13e8799a32b4329b

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line



executor >  local (3)
[bd/f2a4a0] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[62/de9b68] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[-        ] process > make_metafile_unix_friendly    [  0%] 0 of 1
[3e/dbb627] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat Psoriasis.meta.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh Psoriasis.meta.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat Psoriasis.meta.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  tr: write error: Broken pipe
  .command.run: line 23: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/3e/dbb627e640084f13e8799a32b4329b

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line



executor >  local (3)
[bd/f2a4a0] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[62/de9b68] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[-        ] process > make_metafile_unix_friendly    [  0%] 0 of 1
[3e/dbb627] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat Psoriasis.meta.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh Psoriasis.meta.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat Psoriasis.meta.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  tr: write error: Broken pipe
  .command.run: line 23: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/3e/dbb627e640084f13e8799a32b4329b

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line


---
## 58


executor >  local (4)
[f2/405681] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[fd/9503ee] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[4c/8ac2e1] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[42/163b59] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_VEGF_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_VEGF_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_VEGF_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/42/163b592a4df190abbf5aa68e8a712b

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[f2/405681] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[fd/9503ee] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[4c/8ac2e1] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[42/163b59] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_VEGF_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_VEGF_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_VEGF_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/42/163b592a4df190abbf5aa68e8a712b

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[f2/405681] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[fd/9503ee] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[4c/8ac2e1] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[42/163b59] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_VEGF_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_VEGF_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_VEGF_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/42/163b592a4df190abbf5aa68e8a712b

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`


---
## 57

executor >  local (4)
[c0/5d0291] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[3b/666d81] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[30/597f33] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[50/b37898] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_TARC_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_TARC_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_TARC_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/50/b37898013bcb6d141fb01e53f5dd5b

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`



executor >  local (4)
[c0/5d0291] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[3b/666d81] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[30/597f33] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[50/b37898] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_TARC_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_TARC_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_TARC_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/50/b37898013bcb6d141fb01e53f5dd5b

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`



executor >  local (4)
[c0/5d0291] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[3b/666d81] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[30/597f33] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[50/b37898] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_TARC_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_TARC_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_TARC_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/50/b37898013bcb6d141fb01e53f5dd5b

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`



executor >  local (4)
[c0/5d0291] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[3b/666d81] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[30/597f33] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[50/b37898] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_TARC_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_TARC_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_TARC_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/50/b37898013bcb6d141fb01e53f5dd5b

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`



---
## 56


executor >  local (4)
[e0/291d38] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[69/2a995c] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[81/3d7e48] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[cb/aa945c] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_S100b_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_S100b_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_S100b_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/cb/aa945c2e28931fb7842effe1042896

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`



executor >  local (4)
[e0/291d38] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[69/2a995c] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[81/3d7e48] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[cb/aa945c] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_S100b_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_S100b_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_S100b_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/cb/aa945c2e28931fb7842effe1042896

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`



executor >  local (4)
[e0/291d38] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[69/2a995c] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[81/3d7e48] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[cb/aa945c] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_S100b_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_S100b_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_S100b_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/cb/aa945c2e28931fb7842effe1042896

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`

---
## 55


executor >  local (3)
[-        ] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[44/09e2b3] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[38/2ed5cc] process > make_metafile_unix_friendly... [  0%] 0 of 1
[9f/a565c3] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_MCP1_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_MCP1_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_MCP1_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 21: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/9f/a565c3e00fe24ae68ea011c47c219a

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[6b/d218bd] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[44/09e2b3] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[38/2ed5cc] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[9f/a565c3] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_MCP1_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_MCP1_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_MCP1_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 21: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/9f/a565c3e00fe24ae68ea011c47c219a

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[6b/d218bd] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[44/09e2b3] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[38/2ed5cc] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[9f/a565c3] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_MCP1_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_MCP1_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_MCP1_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 21: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/9f/a565c3e00fe24ae68ea011c47c219a

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[6b/d218bd] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[44/09e2b3] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[38/2ed5cc] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[9f/a565c3] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_MCP1_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_MCP1_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_MCP1_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 21: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/9f/a565c3e00fe24ae68ea011c47c219a

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`


---
## 51


executor >  local (4)
[5e/7f26f4] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[0c/49346d] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[88/c179f4] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[fe/15a908] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_EPO_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_EPO_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_EPO_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 21: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/fe/15a9081da43402a1ae59c8038e03da

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`



executor >  local (4)
[5e/7f26f4] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[0c/49346d] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[88/c179f4] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[fe/15a908] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_EPO_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_EPO_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_EPO_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 21: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/fe/15a9081da43402a1ae59c8038e03da

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`



executor >  local (4)
[5e/7f26f4] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[0c/49346d] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[88/c179f4] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[fe/15a908] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_EPO_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_EPO_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_EPO_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 21: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/fe/15a9081da43402a1ae59c8038e03da

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`

---
## 50


executor >  local (4)
[cf/55010d] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[4f/70b3b3] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[a3/63f53b] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[43/632498] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_CRP_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_CRP_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_CRP_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 24: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/43/63249858e454ba7a78a74531a72c15

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line



executor >  local (4)
[cf/55010d] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[4f/70b3b3] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[a3/63f53b] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[43/632498] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_CRP_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_CRP_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_CRP_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 24: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/43/63249858e454ba7a78a74531a72c15

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line



executor >  local (4)
[cf/55010d] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[4f/70b3b3] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[a3/63f53b] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[43/632498] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_CRP_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_CRP_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_CRP_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 24: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/43/63249858e454ba7a78a74531a72c15

Tip: when you have fixed the problem you can continue the execution adding the option `-resume` to the run command line

---
## 49


executor >  local (4)
[60/e38004] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[cc/42358d] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[f4/a42005] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[0a/80365e] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_BDNF_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_BDNF_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_BDNF_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 23: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/0a/80365e46243f4563d9dbb0043ccc42

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`



executor >  local (4)
[60/e38004] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[cc/42358d] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[f4/a42005] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[0a/80365e] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_BDNF_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_BDNF_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_BDNF_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 23: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/0a/80365e46243f4563d9dbb0043ccc42

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`



executor >  local (4)
[60/e38004] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[cc/42358d] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[f4/a42005] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[0a/80365e] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_BDNF_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_BDNF_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_BDNF_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 23: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/0a/80365e46243f4563d9dbb0043ccc42

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`

---
## 53


executor >  local (4)
[c8/f0f248] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[85/15d9b4] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[22/a135e4] process > make_metafile_unix_friendly... [  0%] 0 of 1
[0c/569a81] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_IL18_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_IL18_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_IL18_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/0c/569a81900ef1648280afa4eed51e04

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`



executor >  local (4)
[c8/f0f248] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[85/15d9b4] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[22/a135e4] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[0c/569a81] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_IL18_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_IL18_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_IL18_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/0c/569a81900ef1648280afa4eed51e04

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`



executor >  local (4)
[c8/f0f248] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[85/15d9b4] process > calculate_checksum_on_sumst... [  0%] 0 of 1 ✔
[22/a135e4] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[0c/569a81] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_IL18_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_IL18_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_IL18_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/0c/569a81900ef1648280afa4eed51e04

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`



executor >  local (4)
[c8/f0f248] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[85/15d9b4] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[22/a135e4] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[0c/569a81] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_IL18_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_IL18_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_IL18_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/0c/569a81900ef1648280afa4eed51e04

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`



executor >  local (4)
[c8/f0f248] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[85/15d9b4] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[22/a135e4] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[0c/569a81] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_IL18_num2_SEX_PSYCH2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_IL18_num2_SEX_PSYCH2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_IL18_num2_SEX_PSYCH2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/0c/569a81900ef1648280afa4eed51e04

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`
 
---
## 87


executor >  local (4)
[5d/66b96d] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[50/d662f4] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[0f/841d6a] process > make_metafile_unix_friendly... [  0%] 0 of 1
[4e/61704d] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat pgc.bip.full.2012-04.txt.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh pgc.bip.full.2012-04.txt.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat pgc.bip.full.2012-04.txt.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/4e/61704d59b792320e5c56254aef264f

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[5d/66b96d] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[50/d662f4] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[0f/841d6a] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[4e/61704d] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat pgc.bip.full.2012-04.txt.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh pgc.bip.full.2012-04.txt.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat pgc.bip.full.2012-04.txt.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/4e/61704d59b792320e5c56254aef264f

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[5d/66b96d] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[50/d662f4] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[0f/841d6a] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[4e/61704d] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat pgc.bip.full.2012-04.txt.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh pgc.bip.full.2012-04.txt.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat pgc.bip.full.2012-04.txt.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/4e/61704d59b792320e5c56254aef264f

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`


---
## 79


executor >  local (4)
[29/75dc25] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[22/150353] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[d7/6c1018] process > make_metafile_unix_friendly... [  0%] 0 of 1
[a6/257362] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_NORMENT_BIP_morePC_sts_no45.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_NORMENT_BIP_morePC_sts_no45.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_NORMENT_BIP_morePC_sts_no45.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/a6/25736281b0b5dc1b9f2b5585d71b1c

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[29/75dc25] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[22/150353] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[d7/6c1018] process > make_metafile_unix_friendly... [  0%] 0 of 1
[a6/257362] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_NORMENT_BIP_morePC_sts_no45.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_NORMENT_BIP_morePC_sts_no45.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_NORMENT_BIP_morePC_sts_no45.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/a6/25736281b0b5dc1b9f2b5585d71b1c

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[29/75dc25] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[22/150353] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[d7/6c1018] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[a6/257362] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_NORMENT_BIP_morePC_sts_no45.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_NORMENT_BIP_morePC_sts_no45.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_NORMENT_BIP_morePC_sts_no45.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/a6/25736281b0b5dc1b9f2b5585d71b1c

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[29/75dc25] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[22/150353] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[d7/6c1018] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[a6/257362] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_NORMENT_BIP_morePC_sts_no45.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_NORMENT_BIP_morePC_sts_no45.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_NORMENT_BIP_morePC_sts_no45.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/a6/25736281b0b5dc1b9f2b5585d71b1c

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[29/75dc25] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[22/150353] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[d7/6c1018] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[a6/257362] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_NORMENT_BIP_morePC_sts_no45.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_NORMENT_BIP_morePC_sts_no45.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_NORMENT_BIP_morePC_sts_no45.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/a6/25736281b0b5dc1b9f2b5585d71b1c

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`


---
## 88


executor >  local (4)
[5a/a8f66f] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[51/6bce49] process > calculate_checksum_on_sumst... [  0%] 0 of 1
[0e/633dda] process > make_metafile_unix_friendly... [  0%] 0 of 1
[41/08869e] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_boma_bpd_sample_no_comorbid_2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_boma_bpd_sample_no_comorbid_2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_boma_bpd_sample_no_comorbid_2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/41/08869ebc1671da1f8aff7544ee5cdb

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`



executor >  local (4)
[5a/a8f66f] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[51/6bce49] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[0e/633dda] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[41/08869e] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_boma_bpd_sample_no_comorbid_2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_boma_bpd_sample_no_comorbid_2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_boma_bpd_sample_no_comorbid_2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/41/08869ebc1671da1f8aff7544ee5cdb

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`



executor >  local (4)
[5a/a8f66f] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[51/6bce49] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[0e/633dda] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[41/08869e] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat daner_boma_bpd_sample_no_comorbid_2.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh daner_boma_bpd_sample_no_comorbid_2.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat daner_boma_bpd_sample_no_comorbid_2.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile

Work dir:
  /cleansumstats/tmp/fake-home/work/41/08869ebc1671da1f8aff7544ee5cdb

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`


---
## 91


executor >  local (4)
[4d/0b62ca] process > calculate_checksum_on_metaf... [  0%] 0 of 1
[e4/8b0950] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[dc/c15068] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[96/2b335d] process > check_sumstat_format (1)       [  0%] 0 of 1
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat pgc.mdd.full.2012-04.txt.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh pgc.mdd.full.2012-04.txt.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat pgc.mdd.full.2012-04.txt.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 22: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/96/2b335dad6e44ab12f5de6691e0cf0f

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[4d/0b62ca] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[e4/8b0950] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[dc/c15068] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[96/2b335d] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat pgc.mdd.full.2012-04.txt.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh pgc.mdd.full.2012-04.txt.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat pgc.mdd.full.2012-04.txt.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 22: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/96/2b335dad6e44ab12f5de6691e0cf0f

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`



executor >  local (4)
[4d/0b62ca] process > calculate_checksum_on_metaf... [100%] 1 of 1 ✔
[e4/8b0950] process > calculate_checksum_on_sumst... [100%] 1 of 1 ✔
[dc/c15068] process > make_metafile_unix_friendly... [100%] 1 of 1 ✔
[96/2b335d] process > check_sumstat_format (1)       [100%] 1 of 1, failed: 1 ✘
[-        ] process > add_sorted_rowindex_to_sumstat -
[-        ] process > map_to_dbsnp:prepare_dbsnp_... -
[-        ] process > map_to_dbsnp:remove_duplica... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:is_chrpos_diff... -
[-        ] process > map_to_dbsnp:reformat_chrom... -
[-        ] process > map_to_dbsnp:detect_genome_... -
[-        ] process > map_to_dbsnp:decide_genome_... -
[-        ] process > map_to_dbsnp:build_warning     -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:maplift_dbsnp_... -
[-        ] process > map_to_dbsnp:select_chrpos_... -
[-        ] process > map_to_dbsnp:rm_dup_chrpos_... -
[-        ] process > map_to_dbsnp:reformat_sumstat  -
[-        ] process > map_to_dbsnp:split_multiall... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:allele_co... -
[-        ] process > allele_correction:rm_dup_ch... -
[-        ] process > update_stats:numeric_filter... -
[-        ] process > update_stats:convert_neglogP   -
[-        ] process > update_stats:force_eaf         -
[-        ] process > update_stats:prep_af_stats     -
[-        ] process > update_stats:add_af_stats      -
[-        ] process > update_stats:infer_stats       -
[-        ] process > update_stats:merge_inferred... -
[-        ] process > update_stats:select_stats_f... -
[-        ] process > organize_output:final_assembly -
[-        ] process > organize_output:prep_GRCh37... -
[-        ] process > organize_output:collect_rmd... -
[-        ] process > organize_output:desc_rmd_li... -
[-        ] process > organize_output:gzip_outfiles  -
[-        ] process > organize_output:calculate_c... -
[-        ] process > organize_output:collect_and... -
[-        ] process > organize_output:prepare_cle... -
[-        ] process > organize_output:add_raw_to_... -
[-        ] process > organize_output:add_details... -
[-        ] process > organize_output:add_cleaned... -
Execution cancelled -- Finishing pending tasks before exit
Error executing process > 'check_sumstat_format (1)'

Caused by:
  Process `check_sumstat_format (1)` terminated with an error exit status (1)

Command executed:

  # Sumstat file check on first 1000 lines
  echo "$(head -n 1000 < <(zcat pgc.mdd.full.2012-04.txt.gz))" | gzip -c > check_sumstat_format__sumstat_1000_rows
  check_and_format_sfile.sh check_sumstat_format__sumstat_1000_rows check_sumstat_format__sumstat_1000_rows_formatted check_sumstat_format__sumstat_1000_rows_formatted.log
  
  # Make second sumstat file check on all lines
  check_and_format_sfile.sh pgc.mdd.full.2012-04.txt.gz check_sumstat_format__sumstat_file check_sumstat_format__sumstat_file.log
  
  # Process before and after stats (the -1 is to remove the header count)
  rowsBefore="$(zcat pgc.mdd.full.2012-04.txt.gz | wc -l | awk '{print $1-1}')"
  rowsAfter="$(wc -l check_sumstat_format__sumstat_file | awk '{print $1-1}')"
  echo -e "$rowsBefore	$rowsAfter	Force tab separation" > check_sumstat_format__desc_force_tab_sep_BA.txt

Command exit status:
  1

Command output:
  (empty)

Command error:
  
  gzip: stdout: Broken pipe
  /cleansumstats/bin/check_and_format_sfile.sh: line 86: [: too many arguments
  one or more problems detected with the meta data format, see logfile
  .command.run: line 22: echo: write error: Broken pipe

Work dir:
  /cleansumstats/tmp/fake-home/work/96/2b335dad6e44ab12f5de6691e0cf0f

Tip: you can try to figure out what's wrong by changing to the process work dir and showing the script file named `.command.sh`

```