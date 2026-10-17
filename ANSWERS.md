# Midterm 1: answers

GitHub username:AI-yerassyl
Session code:Kettle-62
Fingerprint:2cbcc8ca

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

(About half a page: which assistants or tools you used and for what. If you used none, say so.)

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A |0.6000|0.6500|0.6667|0.6483|
| B |0.4833|0.7000|0.7333|0.6033|

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 |0.6500|0.5217|0.7599|
| A, k=5 |0.6667|0.5388|0.7744|
| B, k=3 |0.7000|0.5732|0.8034|
| B, k=5 |0.7333|0.6087|0.8305|

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 |14471.71|
| A, k=5 |17442.33|
| B, k=3 |7429.33|
| B, k=5 |8456.54|

### 1d. Decision (at most 150 words)

Chosen candidate: B, k=5

I recommend Config B, k=5. Its cost is 8456.54, well within the 15500 budget. While overall recall intervals for A and B overlap, B5 has the highest absolute recall (0.7333) and strictly beats A3 in MRR (0.6033 / 0.6483). Per language, recall for EN is 0.8667, RU is 0.7500, and KK is 0.6000. The KK (Kazakh) speakers are served worst because the recall for Kazakh is significantly lower than for English and Russian

### 1e. Next measurement (at most 60 words)

Run a larger test set specifically targeting Kazakh (KK) queries to determine if the low per-language recall for B5 is statistically significant or just an artifact of the small sample size

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | | | | | | |
| L | | | | | | |

Personal-data pages per year sent abroad under H:

### 2b. Memo (at most 300 words)

## Part 3: Explain your own numbers

### Q1

Number:
Why (at most 40 words):

### Q2

Number:
Why (at most 40 words):

### Q3

Number:
Why (at most 40 words):

### Q4

Number:
Why (at most 40 words):

### Q5

Number:
Why (at most 40 words):
