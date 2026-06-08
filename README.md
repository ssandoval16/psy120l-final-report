Music and Memory: What Do We Remember When We Feel?
PSY 120L Reproducible Analysis Report

Author
Sarahi Sandoval

Published
June 6, 2026

Concerning This Report The data preparation, variable production, descriptive statistics, principal analysis, and figures for this study are all documented in this reliable report.

The report is meant to go with a research paper in the form of a paper. It is not the entire document. Rather, it demonstrates how a clear and repeatable Quarto technique was used to generate the provided findings from the data.

Study Overview: This study looks at how mood condition, emotional affect, and their interplay effect emotional affect and mood-congruent word memory.

The design included one manipulated independent variable and one measured moderator:

Mood condition: music induced positive induction versus music induced negative induction

Positive and Negative Affect Schedule (PANAS) groups:

Positive Affect Group

Negative affect group -0

The dependent variables were word recall, word recognition, and answer confidence levels.

The primary analyses tested whether mood condition, PANAS score group, and their interaction predicted each outcome.

Setup and Software Environment
This portion of the report loads the packages used in this study for the purposes of: data preparation, scale construction, statistical modeling, estimated marginal means, and figures.

Load Packages

Show code
library(tidyverse)  # data manipulation + plotting
library(psych)      # scale construction + reliability
library(afex)       # ANOVA models + effect sizes
library(emmeans)    # estimated marginal means + confidence intervals

Data Source and Analysis Dataset
Data was collected through an online survey completed on Qualtrics. The imported dataset was saved as study_raw as to preserve the unchanged original file throughout the report.

A smaller analysis dataset was then created for the current analyses called study_data. This dataset selected and cleaned up variable names for analysis and converted all variables, excluding recall items 1, 2, & 3, to numeric format for further preparation.

Import Dataset
Show code
study_raw <- read_csv("data/music_and_memory_data.csv")

Check Imported Dataset
Show code
dim(study_raw)

[1] 107 182
Show code
names(study_raw)

  [1] "StartDate"             "EndDate"               "Status"               
  [4] "IPAddress"             "Progress"              "Duration (in seconds)"
  [7] "Finished"              "RecordedDate"          "ResponseId"           
 [10] "ExternalReference"     "LocationLatitude"      "LocationLongitude"    
 [13] "DistributionChannel"   "UserLanguage"          "Q34"                  
 [16] "Q32_First Click"       "Q32_Last Click"        "Q32_Page Submit"      
 [19] "Q32_Click Count"       "Q33_First Click"       "Q33_Last Click"       
 [22] "Q33_Page Submit"       "Q33_Click Count"       "m_check"              
 [25] "Q52_First Click"       "Q52_Last Click"        "Q52_Page Submit"      
 [28] "Q52_Click Count"       "1_ _First Click"       "1_ _Last Click"       
 [31] "1_ _Page Submit"       "1_ _Click Count"       "2_ _First Click"      
 [34] "2_ _Last Click"        "2_ _Page Submit"       "2_ _Click Count"      
 [37] "4_ _First Click"       "4_ _Last Click"        "4_ _Page Submit"      
 [40] "4_ _Click Count"       "5_ _First Click"       "5_ _Last Click"       
 [43] "5_ _Page Submit"       "5_ _Click Count"       "6_ _First Click"      
 [46] "6_ _Last Click"        "6_ _Page Submit"       "6_ _Click Count"      
 [49] "7_ _First Click"       "7_ _Last Click"        "7_ _Page Submit"      
 [52] "7_ _Click Count"       "recall_1"              "Q47_First Click"      
 [55] "Q47_Last Click"        "Q47_Page Submit"       "Q47_Click Count"      
 [58] "Q74_First Click"       "Q74_Last Click"        "Q74_Page Submit"      
 [61] "Q74_Click Count"       "1_Q45_First Click"     "1_Q45_Last Click"     
 [64] "1_Q45_Page Submit"     "1_Q45_Click Count"     "2_Q45_First Click"    
 [67] "2_Q45_Last Click"      "2_Q45_Page Submit"     "2_Q45_Click Count"    
 [70] "3_Q45_First Click"     "3_Q45_Last Click"      "3_Q45_Page Submit"    
 [73] "3_Q45_Click Count"     "4_Q45_First Click"     "4_Q45_Last Click"     
 [76] "4_Q45_Page Submit"     "4_Q45_Click Count"     "5_Q45_First Click"    
 [79] "5_Q45_Last Click"      "5_Q45_Page Submit"     "5_Q45_Click Count"    
 [82] "6_Q45_First Click"     "6_Q45_Last Click"      "6_Q45_Page Submit"    
 [85] "6_Q45_Click Count"     "7_Q45_First Click"     "7_Q45_Last Click"     
 [88] "7_Q45_Page Submit"     "7_Q45_Click Count"     "recall_2"             
 [91] "Q69_First Click"       "Q69_Last Click"        "Q69_Page Submit"      
 [94] "Q69_Click Count"       "Q76_First Click"       "Q76_Last Click"       
 [97] "Q76_Page Submit"       "Q76_Click Count"       "1_Q46_First Click"    
[100] "1_Q46_Last Click"      "1_Q46_Page Submit"     "1_Q46_Click Count"    
[103] "2_Q46_First Click"     "2_Q46_Last Click"      "2_Q46_Page Submit"    
[106] "2_Q46_Click Count"     "3_Q46_First Click"     "3_Q46_Last Click"     
[109] "3_Q46_Page Submit"     "3_Q46_Click Count"     "4_Q46_First Click"    
[112] "4_Q46_Last Click"      "4_Q46_Page Submit"     "4_Q46_Click Count"    
[115] "5_Q46_First Click"     "5_Q46_Last Click"      "5_Q46_Page Submit"    
[118] "5_Q46_Click Count"     "6_Q46_First Click"     "6_Q46_Last Click"     
[121] "6_Q46_Page Submit"     "6_Q46_Click Count"     "7_Q46_First Click"    
[124] "7_Q46_Last Click"      "7_Q46_Page Submit"     "7_Q46_Click Count"    
[127] "recall_3"              "Q71_First Click"       "Q71_Last Click"       
[130] "Q71_Page Submit"       "Q71_Click Count"       "recognition_1"        
[133] "recognition_2"         "recognition_3"         "recognition_4"        
[136] "recognition_5"         "recognition_6"         "recognition_7"        
[139] "recognition_8"         "recognition_9"         "recognition_10"       
[142] "recognition_11"        "recognition_12"        "recognition_conf_1"   
[145] "recognition_conf_2"    "recognition_conf_3"    "recognition_conf_4"   
[148] "recognition_conf_5"    "recognition_conf_6"    "recognition_conf_7"   
[151] "recognition_conf_8"    "recognition_conf_9"    "recognition_conf_10"  
[154] "recognition_conf_11"   "recognition_conf_12"   "confidence_1"         
[157] "confidence_2"          "confidence_3"          "panas_1"              
[160] "panas_2"               "panas_3"               "panas_4"              
[163] "panas_5"               "panas_6"               "panas_7"              
[166] "panas_8"               "panas_9"               "panas_10"             
[169] "panas_11"              "panas_12"              "panas_13"             
[172] "panas_14"              "panas_15"              "panas_16"             
[175] "panas_17"              "panas_18"              "panas_19"             
[178] "panas_20"              "age"                   "gender"               
[181] "injury"                "music_cond"           
Show code
head(study_raw)

# A tibble: 6 × 182
  StartDate    EndDate Status IPAddress Progress Duration (in seconds…¹ Finished
  <chr>        <chr>    <dbl> <chr>        <dbl>                  <dbl>    <dbl>
1 5/5/26 9:57  5/5/26…      1 <NA>           100                    279        1
2 5/5/26 20:07 5/5/26…      0 146.75.1…      100                    430        1
3 5/5/26 20:11 5/5/26…      0 68.108.2…      100                    302        1
4 5/5/26 20:14 5/5/26…      0 148.222.…      100                    320        1
5 5/5/26 20:13 5/5/26…      0 98.185.2…      100                    473        1
6 5/5/26 20:08 5/5/26…      0 207.171.…      100                    760        1
# ℹ abbreviated name: ¹​`Duration (in seconds)`
# ℹ 175 more variables: RecordedDate <chr>, ResponseId <chr>,
#   ExternalReference <lgl>, LocationLatitude <dbl>, LocationLongitude <dbl>,
#   DistributionChannel <chr>, UserLanguage <chr>, Q34 <dbl>,
#   `Q32_First Click` <dbl>, `Q32_Last Click` <dbl>, `Q32_Page Submit` <dbl>,
#   `Q32_Click Count` <dbl>, `Q33_First Click` <dbl>, `Q33_Last Click` <dbl>,
#   `Q33_Page Submit` <dbl>, `Q33_Click Count` <dbl>, m_check <dbl>, …
The import checks confirms the successful loading of the dataset, the number of rows and columns, and displays the variable names available in the original dataset as well.

Create Analysis Dataset
Show code
study_vars <- c(
  "music_cond", "m_check", "age", "gender", "injury",

"panas_1", "panas_2", "panas_3", "panas_4", "panas_5", "panas_6", "panas_7", "panas_8", "panas_9", "panas_10", "panas_11", "panas_12", "panas_13", "panas_14", "panas_15", "panas_16", "panas_17", "panas_18", "panas_19", "panas_20",

"confidence_1", "confidence_2", "confidence_3",

"recall_1", "recall_2", "recall_3",

"recognition_1", "recognition_2", "recognition_3", "recognition_4", "recognition_5", "recognition_6", "recognition_7", "recognition_8", "recognition_9", "recognition_10", "recognition_11", "recognition_12",

"recognition_conf_1", "recognition_conf_2", "recognition_conf_3", "recognition_conf_4", "recognition_conf_5", "recognition_conf_6", "recognition_conf_7", "recognition_conf_8", "recognition_conf_9", "recognition_conf_10", "recognition_conf_11", "recognition_conf_12"

)



study_data <- study_raw %>%
  select(all_of(study_vars)) %>%
  mutate(
    across(
      -c(recall_1, recall_2, recall_3),
      as.numeric
    )
  )

Check Analysis Dataset
Show code
length(study_vars)

[1] 55
Show code
dim(study_data)

[1] 107  55
Show code
names(study_data)

 [1] "music_cond"          "m_check"             "age"                
 [4] "gender"              "injury"              "panas_1"            
 [7] "panas_2"             "panas_3"             "panas_4"            
[10] "panas_5"             "panas_6"             "panas_7"            
[13] "panas_8"             "panas_9"             "panas_10"           
[16] "panas_11"            "panas_12"            "panas_13"           
[19] "panas_14"            "panas_15"            "panas_16"           
[22] "panas_17"            "panas_18"            "panas_19"           
[25] "panas_20"            "confidence_1"        "confidence_2"       
[28] "confidence_3"        "recall_1"            "recall_2"           
[31] "recall_3"            "recognition_1"       "recognition_2"      
[34] "recognition_3"       "recognition_4"       "recognition_5"      
[37] "recognition_6"       "recognition_7"       "recognition_8"      
[40] "recognition_9"       "recognition_10"      "recognition_11"     
[43] "recognition_12"      "recognition_conf_1"  "recognition_conf_2" 
[46] "recognition_conf_3"  "recognition_conf_4"  "recognition_conf_5" 
[49] "recognition_conf_6"  "recognition_conf_7"  "recognition_conf_8" 
[52] "recognition_conf_9"  "recognition_conf_10" "recognition_conf_11"
[55] "recognition_conf_12"
The analysis dataset showcases the variables required for the report, with the checks confirming the number of selected variables, dimensions of the analysis dataset, and the final variable names carried forward into the preparation and analysis sections.

Variable Preparation
This section of the report shows the preparation of the variables used in the primary analyses. The original imported dataset was left unchanged; all prepared variables were created in the working analysis dataset, study_data.

Count Correct Answers
The free recall responses were open-ended text responses and thus needed to be scored before they could be used as a numeric dependent variable. Each recall response was compared against the target words shown in that block. The code below creates one score for each recall block and then sums those block scores into a total free_recall score, with higher scores indicate that participants correctly recalled more words.

Show code
block_1_words <- c(
  "house", "neglect", "couple", "lantern", "despise", "teacher"
)

block_2_words <- c(
  "coast", "disloyal", "acceptance", "social", "cyclone", "street", "cheer"
)

block_3_words <- c(
  "highway", "grief", "death", "wounds", "desire", "friendly", "strong"
)

score_recall <- function(response, answer_key) {
  
  if (is.na(response)) {
    return(NA_real_)
  }
  
  response_clean <- str_to_lower(response)
  
  recalled_words <- str_extract_all(response_clean, "\\b[a-z]+\\b")[[1]]
  
  sum(answer_key %in% recalled_words)
}

study_data <- study_data %>%
  rowwise() %>%
  mutate(
    recall_1_score = score_recall(recall_1, block_1_words),
    recall_2_score = score_recall(recall_2, block_2_words),
    recall_3_score = score_recall(recall_3, block_3_words),
    free_recall = sum(c(recall_1_score, recall_2_score, recall_3_score), na.rm = TRUE)
  ) %>%
  ungroup()

Check Free Recall Scores
The next chunk checks whether the scoring worked correctly. The block-level recall scores should stay within the possible range for each word list. Because Block 1 had 6 confirmed target words, recall_1_score should range from 0 to 6. Blocks 2 and 3 each had 7 target words, so recall_2_score and recall_3_score should each range from 0 to 7. The total free_recall score should range from 0 to 20.

Show code
study_data %>%
  summarise(
    recall_1_score_min = min(recall_1_score, na.rm = TRUE),
    recall_1_score_max = max(recall_1_score, na.rm = TRUE),
    recall_1_score_mean = mean(recall_1_score, na.rm = TRUE),
    recall_1_score_sd = sd(recall_1_score, na.rm = TRUE),
    
    recall_2_score_min = min(recall_2_score, na.rm = TRUE),
    recall_2_score_max = max(recall_2_score, na.rm = TRUE),
    recall_2_score_mean = mean(recall_2_score, na.rm = TRUE),
    recall_2_score_sd = sd(recall_2_score, na.rm = TRUE),
    
    recall_3_score_min = min(recall_3_score, na.rm = TRUE),
    recall_3_score_max = max(recall_3_score, na.rm = TRUE),
    recall_3_score_mean = mean(recall_3_score, na.rm = TRUE),
    recall_3_score_sd = sd(recall_3_score, na.rm = TRUE),
    
    free_recall_min = min(free_recall, na.rm = TRUE),
    free_recall_max = max(free_recall, na.rm = TRUE),
    free_recall_mean = mean(free_recall, na.rm = TRUE),
    free_recall_sd = sd(free_recall, na.rm = TRUE)
  ) %>%
  pivot_longer(
    cols = everything(),
    names_to = c("variable", ".value"),
    names_pattern = "(.+)_(min|max|mean|sd)"
  ) %>%
  knitr::kable()

variable	min	max	mean	sd
recall_1_score	2	6	4.292453	1.178918
recall_2_score	1	7	3.733333	1.288012
recall_3_score	1	7	4.476191	1.301591
free_recall	0	18	12.308411	3.133541
Prepare Participant ID and Experimental Condition
Show code
study_data <- study_data %>%
  mutate(
    id = row_number(),
    music_cond = factor(
      music_cond,
      levels = c(0, 1),
      labels = c("Negative Condition", "Positive Condition")
    )
  )

The experimental condition variable was recorded as a labeled factor with two levels: negative and positive. Alongside it, a participant ID variable was created so each row was linked to a unique identifier.

Check Experimental Condition Coding
Show code
study_data %>%
  count(music_cond) %>%
  knitr::kable(
    col.names = c("Condition", "n")
  )

Condition	n
Negative Condition	46
Positive Condition	60
NA	1
The condition check confirms the number of participants assigned to each condition, with 46 participants in the negative condition and 60 in the positive, and indicated one missing value in the dataset as well.

Check Prepared Analysis Dataset
Show code
dim(study_data)

[1] 107  60
Show code
names(study_data)

 [1] "music_cond"          "m_check"             "age"                
 [4] "gender"              "injury"              "panas_1"            
 [7] "panas_2"             "panas_3"             "panas_4"            
[10] "panas_5"             "panas_6"             "panas_7"            
[13] "panas_8"             "panas_9"             "panas_10"           
[16] "panas_11"            "panas_12"            "panas_13"           
[19] "panas_14"            "panas_15"            "panas_16"           
[22] "panas_17"            "panas_18"            "panas_19"           
[25] "panas_20"            "confidence_1"        "confidence_2"       
[28] "confidence_3"        "recall_1"            "recall_2"           
[31] "recall_3"            "recognition_1"       "recognition_2"      
[34] "recognition_3"       "recognition_4"       "recognition_5"      
[37] "recognition_6"       "recognition_7"       "recognition_8"      
[40] "recognition_9"       "recognition_10"      "recognition_11"     
[43] "recognition_12"      "recognition_conf_1"  "recognition_conf_2" 
[46] "recognition_conf_3"  "recognition_conf_4"  "recognition_conf_5" 
[49] "recognition_conf_6"  "recognition_conf_7"  "recognition_conf_8" 
[52] "recognition_conf_9"  "recognition_conf_10" "recognition_conf_11"
[55] "recognition_conf_12" "recall_1_score"      "recall_2_score"     
[58] "recall_3_score"      "free_recall"         "id"                 
The prepared analysis dataset contains variables needed for scale construction, descriptive statistics and primary analyses.

Create Scale Scores
Scale item lists were defined and used to compute emotional intensity scores, memory confidence scores, and recognition scores.

Positive and Negative Affect Schedule-Short Form (PANAS-SF) items were defined and used to compute emotional intensity score by taking the row mean of the 20 PANAS-SF items.

Memory confidence scores were computed as the average of three confidence items.

Recognition confidence scores were computed as the average of the 12 recognition confidence items.

Show code
# PANAS emotional state/intensity items
panas_items <- c(
  "panas_1", "panas_2", "panas_3", "panas_4", "panas_5",
  "panas_6", "panas_7", "panas_8", "panas_9", "panas_10",
  "panas_11", "panas_12", "panas_13", "panas_14", "panas_15",
  "panas_16", "panas_17", "panas_18", "panas_19", "panas_20"
)

# Memory confidence items
confidence_items <- c(
  "confidence_1",
  "confidence_2",
  "confidence_3"
)

# Recognition accuracy items
recognition_items <- c(
  "recognition_1", "recognition_2", "recognition_3", "recognition_4",
  "recognition_5", "recognition_6", "recognition_7", "recognition_8",
  "recognition_9", "recognition_10", "recognition_11", "recognition_12"
)

# Recognition confidence items
recognition_conf_items <- c(
  "recognition_conf_1", "recognition_conf_2", "recognition_conf_3",
  "recognition_conf_4", "recognition_conf_5", "recognition_conf_6",
  "recognition_conf_7", "recognition_conf_8", "recognition_conf_9",
  "recognition_conf_10", "recognition_conf_11", "recognition_conf_12"
)

# Correct recognition answers
# 1 = Yes
# 2 = No
recognition_key <- c(
  recognition_1 = 2,
  recognition_2 = 1,
  recognition_3 = 1,
  recognition_4 = 2,
  recognition_5 = 1,
  recognition_6 = 1,
  recognition_7 = 1,
  recognition_8 = 1,
  recognition_9 = 1,
  recognition_10 = 1,
  recognition_11 = 2,
  recognition_12 = 1
)

# Recognition score variable names
recognition_score_items <- paste0(recognition_items, "_score")

study_data <- study_data %>%
  mutate(
    emotional_state_intensity = rowMeans(across(all_of(panas_items)), na.rm = TRUE),
    memory_confidence = rowMeans(across(all_of(confidence_items)), na.rm = TRUE),
    recognition_confidence = rowMeans(across(all_of(recognition_conf_items)), na.rm = TRUE)
  ) %>%
  mutate(
    across(
      all_of(recognition_items),
      ~ if_else(.x == recognition_key[cur_column()], 1, 0),
      .names = "{.col}_score"
    )
  ) %>%
  mutate(
    recognition_accuracy = rowMeans(across(all_of(recognition_score_items)), na.rm = TRUE)
  )

Check Scale Scores
Show code
study_data %>%
  select(
    emotional_state_intensity,
    memory_confidence,
    recognition_accuracy,
    recognition_confidence,
    free_recall
  ) %>%
  summary()

 emotional_state_intensity memory_confidence recognition_accuracy
 Min.   :1.050             Min.   : 22.00    Min.   :0.00000     
 1st Qu.:1.600             1st Qu.: 50.67    1st Qu.:0.00000     
 Median :2.050             Median : 64.33    Median :0.08333     
 Mean   :2.057             Mean   : 62.63    Mean   :0.11825     
 3rd Qu.:2.400             3rd Qu.: 74.67    3rd Qu.:0.16667     
 Max.   :4.000             Max.   :100.00    Max.   :0.58333     
 NAs    :2                 NAs    :2         NAs    :2           
 recognition_confidence  free_recall   
 Min.   :1.000          Min.   : 0.00  
 1st Qu.:1.750          1st Qu.:11.00  
 Median :1.917          Median :13.00  
 Mean   :1.836          Mean   :12.31  
 3rd Qu.:1.917          3rd Qu.:14.00  
 Max.   :2.000          Max.   :18.00  
 NAs    :2                             
Show code
study_data %>%
  summarise(
    emotional_state_intensity_missing = mean(is.na(emotional_state_intensity)),
    memory_confidence_missing = mean(is.na(memory_confidence)),
    recognition_accuracy_missing = mean(is.na(recognition_accuracy)),
    recognition_confidence_missing = mean(is.na(recognition_confidence)),
    free_recall_missing = mean(is.na(free_recall))
  ) %>%
  knitr::kable()

emotional_state_intensity_missing	memory_confidence_missing	recognition_accuracy_missing	recognition_confidence_missing	free_recall_missing
0.0186916	0.0186916	0.0186916	0.0186916	0
The scale-score checks confirm that computed scale scores are within the expected response range and show missing scale scores as well.

Create Emotional Intensity Groups
A low/high emotional intensity grouping variable was created for the planned 2x2 ANOVA models. Participants with emotional intensity scores at or below the sample median were assigned to the Low group whilst participants above the sample median were assigned to the High group.

Show code
emotional_state_median <- median(
  study_data$emotional_state_intensity,
  na.rm = TRUE
)

study_data <- study_data %>%
  mutate(
    emotional_state_group = if_else(
      emotional_state_intensity <= emotional_state_median,
      "Low",
      "High"
    ),
    emotional_state_group = factor(
      emotional_state_group,
      levels = c("Low", "High")
    )
  )

emotional_state_median

[1] 2.05
Show code
study_data %>%
  count(emotional_state_group) %>%
  knitr::kable()

emotional_state_group	n
Low	56
High	49
NA	2
The median split created the emotional affect grouping variable used in our primary ANOVA models, with the output reporting the median value used for the split and the number of participants assigned to each emotional affect group. The output also reported two missing values.

Check Scale Reliability
Internal consistency was estimated for the affect intensity, memory confidence, and recognition confidence scales prior to being used for analysis.

Show code
# Create item-only data frames for each multi-item rating scale
panas_item_df <- study_data %>% 
  select(all_of(panas_items))

confidence_item_df <- study_data %>% 
  select(all_of(confidence_items))

recognition_conf_item_df <- study_data %>% 
  select(all_of(recognition_conf_items))

# Compute internal consistency estimates
panas_alpha <- psych::alpha(panas_item_df)
panas_omega <- psych::omega(panas_item_df, plot = FALSE)

confidence_alpha <- psych::alpha(confidence_item_df)
confidence_omega <- psych::omega(confidence_item_df, plot = FALSE)

recognition_conf_alpha <- psych::alpha(recognition_conf_item_df)
recognition_conf_omega <- psych::omega(recognition_conf_item_df, plot = FALSE)

# Print only alpha and omega coefficients
tibble(
  scale = c(
    "Emotional State Intensity",
    "Memory Confidence",
    "Recognition Confidence"
  ),
  alpha = c(
    panas_alpha$total$raw_alpha,
    confidence_alpha$total$raw_alpha,
    recognition_conf_alpha$total$raw_alpha
  ),
  omega = c(
    panas_omega$omega.tot,
    confidence_omega$omega.tot,
    recognition_conf_omega$omega.tot
  )
) %>%
  knitr::kable(col.names = c("Scale", "Cronbach's alpha", "McDonald's Omega"))

Scale	Cronbach’s alpha	McDonald’s Omega
Emotional State Intensity	0.8876551	0.9243495
Memory Confidence	0.7363944	0.7606041
Recognition Confidence	0.6685002	0.7598670
The reliability table reports Cronbach’s alpha and McDonald’s omega for each scale used in the analysis.

Descriptive Statistics
This section summarizes the scale scores and sample composition before analysis is conducted.

Scale Score Descriptives
Show code
study_data %>%
  select(
    emotional_state_intensity,
    memory_confidence,
    recognition_confidence,
    recognition_accuracy,
    free_recall
  ) %>%
  psych::describe() %>%
  knitr::kable(digits = 2)

vars	n	mean	sd	median	trimmed	mad	min	max	range	skew	kurtosis	se
emotional_state_intensity	1	105	2.06	0.60	2.05	2.03	0.59	1.05	4.00	2.95	0.52	0.03	0.06
memory_confidence	2	105	62.63	17.09	64.33	63.16	16.80	22.00	100.00	78.00	-0.22	-0.48	1.67
recognition_confidence	3	105	1.84	0.18	1.92	1.87	0.12	1.00	2.00	1.00	-2.23	6.88	0.02
recognition_accuracy	4	105	0.12	0.11	0.08	0.11	0.12	0.00	0.58	0.58	1.14	1.87	0.01
free_recall	5	107	12.31	3.13	13.00	12.40	2.97	0.00	18.00	18.00	-0.66	1.44	0.30
The table shows descriptive statistics for the emotional affect, memory confidence, recognition confidence, recognition accuracy, and free recall scores used in the primary analyses.

Sample Composition by Age, Gender, and Injury
Show code
study_data %>%
  summarise(
    mean_age = mean(age, na.rm = TRUE),
    sd_age = sd(age, na.rm = TRUE),
    min_age = min(age, na.rm = TRUE),
    max_age = max(age, na.rm = TRUE)
  ) %>%
  knitr::kable(
    digits = 2,
    col.names = c("Mean", "SD", "Minimum", "Maximum"),
    caption = "Sample Age: Mean, Standard Deviation, and Range"
  )

Sample Age: Mean, Standard Deviation, and Range
Mean	SD	Minimum	Maximum
22.54	4.68	16	52
Show code
study_data %>%
  count(gender) %>%
  arrange(gender) %>%
  mutate(percent = round(100 * n / sum(n), 1)) %>%
  knitr::kable(
    col.names = c("Gender", "n", "Percent"),
    caption = "Sample Composition by Gender"
  )

Sample Composition by Gender
Gender	n	Percent
1	32	29.9
2	72	67.3
3	1	0.9
NA	2	1.9
Show code
study_data %>%
  count(injury) %>%
  arrange(injury) %>%
  mutate(percent = round(100 * n / sum(n), 1)) %>%
  knitr::kable(
    col.names = c("Neurological Condition or Brain Injury", "n", "Percent"),
    caption = "Sample Composition by Neurological Condition or Brain Injury"
  )

Sample Composition by Neurological Condition or Brain Injury
Neurological Condition or Brain Injury	n	Percent
1	4	3.7
2	96	89.7
3	1	0.9
NA	6	5.6
The sample composition tables above summarizes demographic variables, including mean, standard deviation, and the range of age, and the number and percentage of participants in each gender category and neurological condition group (whether or not you have had a debilitating neurological condition/brain injury) as well.

Correlations Among the DVs
This section examines correlations for the main continuous study variables.

Show code
# Correlations for the main continuous study variables
psych::corr.test(
  study_data %>% 
    select(
      emotional_state_intensity,
      memory_confidence,
      recognition_confidence,
      recognition_accuracy,
      free_recall
    )
)

Call:psych::corr.test(x = study_data %>% select(emotional_state_intensity, 
    memory_confidence, recognition_confidence, recognition_accuracy, 
    free_recall))
Correlation matrix 
                          emotional_state_intensity memory_confidence
emotional_state_intensity                      1.00              0.03
memory_confidence                              0.03              1.00
recognition_confidence                         0.18              0.39
recognition_accuracy                          -0.03             -0.06
free_recall                                    0.13              0.47
                          recognition_confidence recognition_accuracy
emotional_state_intensity                   0.18                -0.03
memory_confidence                           0.39                -0.06
recognition_confidence                      1.00                -0.21
recognition_accuracy                       -0.21                 1.00
free_recall                                 0.37                -0.33
                          free_recall
emotional_state_intensity        0.13
memory_confidence                0.47
recognition_confidence           0.37
recognition_accuracy            -0.33
free_recall                      1.00
Sample Size 
                          emotional_state_intensity memory_confidence
emotional_state_intensity                       105               105
memory_confidence                               105               105
recognition_confidence                          105               105
recognition_accuracy                            105               105
free_recall                                     105               105
                          recognition_confidence recognition_accuracy
emotional_state_intensity                    105                  105
memory_confidence                            105                  105
recognition_confidence                       105                  105
recognition_accuracy                         105                  105
free_recall                                  105                  105
                          free_recall
emotional_state_intensity         105
memory_confidence                 105
recognition_confidence            105
recognition_accuracy              105
free_recall                       107
Probability values (Entries above the diagonal are adjusted for multiple tests.) 
                          emotional_state_intensity memory_confidence
emotional_state_intensity                      0.00              1.00
memory_confidence                              0.80              0.00
recognition_confidence                         0.07              0.00
recognition_accuracy                           0.77              0.56
free_recall                                    0.18              0.00
                          recognition_confidence recognition_accuracy
emotional_state_intensity                   0.34                 1.00
memory_confidence                           0.00                 1.00
recognition_confidence                      0.00                 0.17
recognition_accuracy                        0.03                 0.00
free_recall                                 0.00                 0.00
                          free_recall
emotional_state_intensity        0.73
memory_confidence                0.00
recognition_confidence           0.00
recognition_accuracy             0.00
free_recall                      0.00

 To see confidence intervals of the correlations, print with the short=FALSE option
Primary Analyses
This section reports the primary analyses used to test whether mood condition, emotional affect intensity, and their interaction predicted mood-congruent word memory performance.

Two 2x2 ANOVA models were estimated. The first model used free recall scores as the dependent variable and the second model used recognition accuracy. In both models, mood condition (positive versus negative) was the manipulated independent variable and emotional affect intensity was the moderator.

Free Recall Model
A 2x2 ANOVA tested whether free recall scores differed by mood condition, emotional affect group, and the mood condition x emotional affect group interaction.

Show code
# Create a participant ID variable for the ANOVA
study_data <- study_data %>%
  mutate(id = row_number())

# 2x2 between-subjects ANOVA predicting free recall scores
# DV: free_recall
# Factors: music_cond and emotional_state_group
a1_free_recall <- afex::aov_ez(
  id = "id",
  dv = "free_recall",
  between = c("music_cond", "emotional_state_group"),
  data = study_data
)

# Print the ANOVA table
a1_free_recall

Anova Table (Type 3 tests)

Response: free_recall
                            Effect     df  MSE    F  ges p.value
1                       music_cond 1, 101 7.81 0.27 .003    .607
2            emotional_state_group 1, 101 7.81 0.54 .005    .462
3 music_cond:emotional_state_group 1, 101 7.81 0.18 .002    .674
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '+' 0.1 ' ' 1
The ANOVA table above reports the main effect of mood condition, the main effect of emotional affect group, and the mood condition x emotional affect group interaction for free recall scores.

Estimated Means for Free Recall
Show code
emmeans(a1_free_recall, ~ music_cond)

 music_cond         emmean    SE  df lower.CL upper.CL
 Negative Condition   12.7 0.412 101     11.9     13.5
 Positive Condition   12.4 0.367 101     11.7     13.1

Results are averaged over the levels of: emotional_state_group 
Confidence level used: 0.95 
Show code
emmeans(a1_free_recall, ~ emotional_state_group)

 emotional_state_group emmean   SE  df lower.CL upper.CL
 Low                     12.3 0.38 101     11.6     13.1
 High                    12.8 0.40 101     12.0     13.6

Results are averaged over the levels of: music_cond 
Confidence level used: 0.95 
Show code
emmeans(a1_free_recall, ~ music_cond * emotional_state_group)

 music_cond         emotional_state_group emmean    SE  df lower.CL upper.CL
 Negative Condition Low                     12.6 0.583 101     11.5     13.8
 Positive Condition Low                     12.1 0.487 101     11.1     13.1
 Negative Condition High                    12.8 0.583 101     11.6     13.9
 Positive Condition High                    12.7 0.548 101     11.6     13.8

Confidence level used: 0.95 
The estimated means show the free recall score pattern across mood condition, emotional affect intensity group, and their combined cells.

Recognition Accuracy Model
The second 2x2 ANOVA tested whether recognition accuracy scores differed by mood condition, emotional affect group, and the mood condition x emotional affect group interaction.

Show code
# 2x2 between-subjects ANOVA predicting recognition accuracy
# DV: recognition_accuracy
# Factors: music_cond and emotional_state_group
a2_recognition_accuracy <- afex::aov_ez(
  id = "id",
  dv = "recognition_accuracy",
  between = c("music_cond", "emotional_state_group"),
  data = study_data
)

# Print the ANOVA table
a2_recognition_accuracy

Anova Table (Type 3 tests)

Response: recognition_accuracy
                            Effect     df  MSE    F   ges p.value
1                       music_cond 1, 101 0.01 0.00 <.001    .995
2            emotional_state_group 1, 101 0.01 0.94  .009    .333
3 music_cond:emotional_state_group 1, 101 0.01 0.03 <.001    .854
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '+' 0.1 ' ' 1
The ANOVA table above reports the main effect of mood condition, the main effect of emotional affect group, and the mood condition x emotional affect group interaction for recognition accuracy scores.

Estimated Means for Recognition
Show code
emmeans(a2_recognition_accuracy, ~ music_cond)

 music_cond         emmean     SE  df lower.CL upper.CL
 Negative Condition  0.118 0.0164 101   0.0852    0.150
 Positive Condition  0.118 0.0146 101   0.0887    0.147

Results are averaged over the levels of: emotional_state_group 
Confidence level used: 0.95 
Show code
emmeans(a2_recognition_accuracy, ~ emotional_state_group)

 emotional_state_group emmean     SE  df lower.CL upper.CL
 Low                    0.128 0.0151 101   0.0984    0.158
 High                   0.107 0.0159 101   0.0754    0.139

Results are averaged over the levels of: music_cond 
Confidence level used: 0.95 
Show code
emmeans(a2_recognition_accuracy, ~ music_cond * emotional_state_group)

 music_cond         emotional_state_group emmean     SE  df lower.CL upper.CL
 Negative Condition Low                    0.130 0.0232 101   0.0844    0.176
 Positive Condition Low                    0.126 0.0194 101   0.0879    0.165
 Negative Condition High                   0.105 0.0232 101   0.0591    0.151
 Positive Condition High                   0.109 0.0218 101   0.0657    0.152

Confidence level used: 0.95 
The estimated means show the recognition accuracy score pattern across mood condition, emotional affect intensity group, and their combined cells.

Memory Confidence ANOVA
The third 2x2 ANOVA tested whether memory confidence scores differed by mood condition, emotional affect group, and the mood condition x emotional affect group interaction.

Show code
# 2x2 between-subjects ANOVA predicting memory confidence
# DV: memory_confidence
# Factors: music_cond and emotional_state_group
a3_memory_confidence <- afex::aov_ez(
  id = "id",
  dv = "memory_confidence",
  between = c("music_cond", "emotional_state_group"),
  data = study_data
)

# Print the ANOVA table
a3_memory_confidence

Anova Table (Type 3 tests)

Response: memory_confidence
                            Effect     df    MSE      F  ges p.value
1                       music_cond 1, 101 288.58 2.83 + .027    .095
2            emotional_state_group 1, 101 288.58   0.57 .006    .452
3 music_cond:emotional_state_group 1, 101 288.58   1.00 .010    .320
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '+' 0.1 ' ' 1
The ANOVA table above reports the effect of mood condition, the effect of emotional affect group, and the mood condition x emotional affect group interaction for memory confidence scores.

Estimated Means for Memory Confidence
Show code
emmeans(a3_memory_confidence, ~ music_cond)

 music_cond         emmean   SE  df lower.CL upper.CL
 Negative Condition   65.8 2.50 101     60.8     70.7
 Positive Condition   60.1 2.23 101     55.7     64.5

Results are averaged over the levels of: emotional_state_group 
Confidence level used: 0.95 
Show code
emmeans(a3_memory_confidence, ~ emotional_state_group)

 emotional_state_group emmean   SE  df lower.CL upper.CL
 Low                     61.7 2.31 101     57.1     66.3
 High                    64.2 2.43 101     59.4     69.0

Results are averaged over the levels of: music_cond 
Confidence level used: 0.95 
Show code
emmeans(a3_memory_confidence, ~ music_cond * emotional_state_group)

 music_cond         emotional_state_group emmean   SE  df lower.CL upper.CL
 Negative Condition Low                     62.8 3.54 101     55.8     69.9
 Positive Condition Low                     60.5 2.96 101     54.7     66.4
 Negative Condition High                    68.7 3.54 101     61.7     75.7
 Positive Condition High                    59.7 3.33 101     53.1     66.3

Confidence level used: 0.95 
The estimated means show the memory confidence score pattern across mood condition, emotional affect intensity group, and their combined cells.

Recognition Confidence ANOVA
The last 2x2 ANOVA tested whether recognition confidence scores differed by mood condition, emotional affect group, and the mood condition x emotional affect group interaction.

Show code
# 2x2 between-subjects ANOVA predicting recognition confidence
# DV: recognition_confidence
# Factors: music_cond and emotional_state_group
a4_recognition_confidence <- afex::aov_ez(
  id = "id",
  dv = "recognition_confidence",
  between = c("music_cond", "emotional_state_group"),
  data = study_data
)

# Print the ANOVA table
a4_recognition_confidence

Anova Table (Type 3 tests)

Response: recognition_confidence
                            Effect     df  MSE      F   ges p.value
1                       music_cond 1, 101 0.03   0.07 <.001    .788
2            emotional_state_group 1, 101 0.03 3.21 +  .031    .076
3 music_cond:emotional_state_group 1, 101 0.03   0.00 <.001    .961
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '+' 0.1 ' ' 1
The ANOVA table above reports the effect of mood condition, the effect of emotional affect group, and the mood condition x emotional affect group interaction for recognition confidence scores.

Estimated Means for Recognition Confidence
Show code
emmeans(a4_recognition_confidence, ~ music_cond)

 music_cond         emmean     SE  df lower.CL upper.CL
 Negative Condition   1.84 0.0267 101     1.79     1.90
 Positive Condition   1.83 0.0238 101     1.79     1.88

Results are averaged over the levels of: emotional_state_group 
Confidence level used: 0.95 
Show code
emmeans(a4_recognition_confidence, ~ emotional_state_group)

 emotional_state_group emmean     SE  df lower.CL upper.CL
 Low                     1.81 0.0246 101     1.76     1.86
 High                    1.87 0.0259 101     1.82     1.92

Results are averaged over the levels of: music_cond 
Confidence level used: 0.95 
Show code
emmeans(a4_recognition_confidence, ~ music_cond * emotional_state_group)

 music_cond         emotional_state_group emmean     SE  df lower.CL upper.CL
 Negative Condition Low                     1.81 0.0378 101     1.74     1.89
 Positive Condition Low                     1.80 0.0316 101     1.74     1.87
 Negative Condition High                    1.88 0.0378 101     1.80     1.95
 Positive Condition High                    1.87 0.0356 101     1.79     1.94

Confidence level used: 0.95 
The estimated means show the recognition confidence score pattern across mood condition, emotional affect intensity group, and their combined cells.

Figures
This section showcases the figures used to visualize the primary 2x2 ANOVA results, with figures based on the estimated cell means from the ANOVA models.

Free Recall Interaction Plot
Show code


The figure shows mean free recall scores by music condition and emotional affect group, with error bars representing 95% confidence intervals.

Recognition Accuracy Interaction Plot
Show code
p_recognition_accuracy_bar <- ggplot(
  as.data.frame(emmeans(a2_recognition_accuracy, ~ music_cond * emotional_state_group)),
  aes(
    x = music_cond,
    y = emmean,
    fill = emotional_state_group
  )
) +
  geom_col(
    position = position_dodge(width = 0.65),
    width = 0.55,
    color = "white"
  ) +
  geom_errorbar(
    aes(
      ymin = lower.CL,
      ymax = upper.CL
    ),
    position = position_dodge(width = 0.65),
    width = 0.12,
    linewidth = 0.7
  ) +
  labs(
    x = "Music Condition",
    y = "Mean Recognition Accuracy",
    fill = "Emotional Affect Group"
  ) +
  scale_x_discrete(labels = c("Negative", "Positive")) +
  scale_fill_manual(
    values = c(
      "Low" = "#E76F51",
      "High" = "#2A9D8F"
    )
  ) +
  scale_y_continuous(
    breaks = seq(0, 1, 0.1)
  ) +
  coord_cartesian(
    ylim = c(0, 1)
  ) +
  theme_classic(
    base_size = 14
  )

p_recognition_accuracy_bar



The figure shows mean recognition accuracy scores by music condition and emotional affect group, with error bars representing 95% confidence intervals.

Memory Confidence Interaction Plot
Show code
p_memory_confidence_bar <- ggplot(
  as.data.frame(emmeans(a3_memory_confidence, ~ music_cond * emotional_state_group)),
  aes(
    x = music_cond,
    y = emmean,
    fill = emotional_state_group
  )
) +
  geom_col(
    position = position_dodge(width = 0.65),
    width = 0.55,
    color = "white"
  ) +
  geom_errorbar(
    aes(
      ymin = lower.CL,
      ymax = upper.CL
    ),
    position = position_dodge(width = 0.65),
    width = 0.12,
    linewidth = 0.7
  ) +
  labs(
    x = "Music Condition",
    y = "Mean Memory Confidence",
    fill = "Emotional Affect Group"
  ) +
  scale_x_discrete(labels = c("Negative", "Positive")) +
  scale_fill_manual(
    values = c(
      "Low" = "#E76F51",
      "High" = "#2A9D8F"
    )
  ) +
  scale_y_continuous(
    breaks = seq(0, 100, 10)
  ) +
  coord_cartesian(
    ylim = c(0, 100)
  ) +
  theme_classic(
    base_size = 14
  )

p_memory_confidence_bar



The figure shows mean memory confidence scores by music condition and emotional affect group, with error bars representing 95% confidence intervals.

Recognition Confidence Interaction Plot
Show code
p_recognition_confidence_bar <- ggplot(
  as.data.frame(emmeans(a4_recognition_confidence, ~ music_cond * emotional_state_group)),
  aes(
    x = music_cond,
    y = emmean,
    fill = emotional_state_group
  )
) +
  geom_col(
    position = position_dodge(width = 0.65),
    width = 0.55,
    color = "white"
  ) +
  geom_errorbar(
    aes(
      ymin = lower.CL,
      ymax = upper.CL
    ),
    position = position_dodge(width = 0.65),
    width = 0.12,
    linewidth = 0.7
  ) +
  labs(
    x = "Music Condition",
    y = "Mean Recognition Confidence",
    fill = "Emotional Affect Group"
  ) +
  scale_x_discrete(labels = c("Negative", "Positive")) +
  scale_fill_manual(
    values = c(
      "Low" = "#E76F51",
      "High" = "#2A9D8F"
    )
  ) +
  scale_y_continuous(
    breaks = seq(1, 5, 1)
  ) +
  coord_cartesian(
    ylim = c(1, 5)
  ) +
  theme_classic(
    base_size = 14
  )

p_recognition_confidence_bar



The figure shows mean recognition confidence scores by music condition and emotional affect group, with error bars representing 95% confidence intervals.

Export Figures
Show code
if (!dir.exists("figures")) {
  dir.create("figures")
}

ggsave(
  filename = "figures/free_recall_interaction_plot.svg",
  plot = p_free_recall_bar,
  width = 7,
  height = 5
)

ggsave(
  filename = "figures/recognition_accuracy_interaction_plot.svg",
  plot = p_recognition_accuracy_bar,
  width = 7,
  height = 5
)

ggsave(
  filename = "figures/memory_confidence_interaction_plot.svg",
  plot = p_memory_confidence_bar,
  width = 7,
  height = 5
)

ggsave(
  filename = "figures/recognition_confidence_interaction_plot.svg",
  plot = p_recognition_confidence_bar,
  width = 7,
  height = 5
)

The created figures were exported to the figures/ folder to be kept for further use in manuscript, poster, or repository materials concerning this study.

Results Summary
The primary analyses tested whether mood condition, emotional affect group, and their interaction predicted mood-congruent word memory performance. Across the free recall and recognition performance ANOVA models, neither mood condition nor emotional affect group were statistically significant in predicting mood-congruent word memory performance. Participants did not significantly differ in free recall memory scores or recognition accuracy scores in regards of either mood induction or emotional affect intensity.

The interaction between music conditioning and emotional affect group was not statistically significant, indicating that the effect of music conditioning on mood-congruent word memory did not meaningfully differ across levels of emotional affect intensity. The estimated means and interaction plots shown above provide the full model output and visualize the pattern of results for each outcome.

Reproducibility Information
This section contains the version of R, operating system, and the package versions used to provide this report, with the inclusion of this information aiming to help others easily identify the software used to portray the analyses provided.

Show code
sessionInfo()

R version 4.6.0 (2026-04-24)
Platform: aarch64-apple-darwin23
Running under: macOS Sonoma 14.8.3

Matrix products: default
BLAS:   /Library/Frameworks/R.framework/Versions/4.6/Resources/lib/libRblas.0.dylib 
LAPACK: /Library/Frameworks/R.framework/Versions/4.6/Resources/lib/libRlapack.dylib;  LAPACK version 3.12.1

locale:
[1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8

time zone: America/Los_Angeles
tzcode source: internal

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
 [1] emmeans_2.0.3   afex_1.5-1      lme4_2.0-1      Matrix_1.7-5   
 [5] psych_2.6.3     lubridate_1.9.5 forcats_1.0.1   stringr_1.6.0  
 [9] dplyr_1.2.1     purrr_1.2.2     readr_2.2.0     tidyr_1.3.2    
[13] tibble_3.3.1    ggplot2_4.0.3   tidyverse_2.0.0

loaded via a namespace (and not attached):
 [1] gtable_0.3.6         xfun_0.57            lattice_0.22-9      
 [4] tzdb_0.5.0           numDeriv_2016.8-1.1  vctrs_0.7.3         
 [7] tools_4.6.0          Rdpack_2.6.6         generics_0.1.4      
[10] parallel_4.6.0       pkgconfig_2.0.3      RColorBrewer_1.1-3  
[13] S7_0.2.2             lifecycle_1.0.5      GPArotation_2025.3-1
[16] compiler_4.6.0       farver_2.1.2         textshaping_1.0.5   
[19] mnormt_2.1.2         lmerTest_3.2-1       carData_3.0-6       
[22] htmltools_0.5.9      yaml_2.3.12          Formula_1.2-5       
[25] crayon_1.5.3         pillar_1.11.1        car_3.1-5           
[28] nloptr_2.2.1         MASS_7.3-65          reformulas_0.4.4    
[31] boot_1.3-32          abind_1.4-8          nlme_3.1-169        
[34] tidyselect_1.2.1     digest_0.6.39        mvtnorm_1.3-7       
[37] stringi_1.8.7        reshape2_1.4.5       splines_4.6.0       
[40] fastmap_1.2.0        grid_4.6.0           cli_3.6.6           
[43] magrittr_2.0.5       utf8_1.2.6           withr_3.0.2         
[46] scales_1.4.0         bit64_4.8.0          timechange_0.4.0    
[49] estimability_1.5.1   rmarkdown_2.31       bit_4.6.0           
[52] ragg_1.5.2           hms_1.1.4            evaluate_1.0.5      
[55] knitr_1.51           rbibutils_2.4.1      rlang_1.2.0         
[58] Rcpp_1.1.1-1.1       glue_1.8.1           svglite_2.2.2       
[61] vroom_1.7.1          rstudioapi_0.18.0    minqa_1.2.8         
[64] jsonlite_2.0.0       R6_2.6.1             plyr_1.8.9          
[67] systemfonts_1.3.2  
