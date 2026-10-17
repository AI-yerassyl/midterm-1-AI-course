# Midterm 1: answers

GitHub username:AI-yerassyl
Session code:Kettle-62
Fingerprint:2cbcc8ca

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

## Заявление об использовании ИИ

Во время мидки использовал одного ИИ-помощника: Клода, не использовал никаких других инструментов ИИ кроме нее

Сначала я вставил свои данные (DATA.md, таблицу рангов, результаты документа) в чат и написал свою первую версию ANSWERS.md. Затем я отправил свои ответы Клоду и попросил его проверить их. Он обнаружил несколько ошибок в моей работе. Стоимость конвейера H была неверной, потому что я неправильно посчитал токены изображений. Общая точность была немного неточной. Вопрос 3 был неверным, вопрос 5 был пустым, а объяснение в вопросе 1 было неверным. Некоторые из моих чисел в части 1 также не соответствовали данными

После этого Клод пересчитал числа с помощью Python и предоставил мне исправленную версию ответов. Он также переписал решение в 1d, следующее измерение в 1e, примечание в 2b и строки «Почему» в части 3. Он показал мне, как примечание должно соответствовать рубрике README. Я прочитал эти тексты и решил их использовать

Чтобы проверить цифры самостоятельно, я запустил скрипт в своем блокноте Colab для проверки полноты ответа, MRR и интервалов Вильсона. Результаты совпали с результатами Клода. Я также проверил свой отпечаток пальца в файле DATA.md.

Я понимаю, что несу ответственность за все данные в этом файле, и могу объяснить свои ответы на устном экзамене )

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A |0.5833|0.6667|0.7500|0.6422|
| B |0.3000|0.6167|0.6667|0.4552|

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 |0.6667|0.5406|0.7727|
| A, k=5 |0.7500|0.6277|0.8422|
| B, k=3 |0.6167|0.4902|0.7291|
| B, k=5 |0.6667|0.5406|0.7727|

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 |13082.32|
| A, k=5 |17912.19|
| B, k=3 |7792.55|
| B, k=5 |9095.90|

### 1d. Decision (at most 150 words)

Chosen candidate: B, k=5

A,k=5 has the best recall (0.75) but costs 17,912, above the 15,500 budget, so it is out. A,k=3 and B,k=5 have identical recall (0.6667, interval 0.54–0.77), but B,k=5 costs 9,096 against 13,082, about 30 % less. All intervals overlap, so no candidate is shown to beat another; I choose on cost at equal recall. MRR matters little because all k chunks go into the prompt. Recall of B,k=5 by language: EN 0.75, RU 0.55, KK 0.70. Russian is served worst

### 1e. Next measurement (at most 60 words)

Collect a larger test set with at least 100 questions per language and compare A,k=3 with B,k=5 on the same questions. Check whether Russian recall (0.55 on 20 questions) is really lower or just sampling noise

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H |0.8778|KK, degraded|0.8000|0.6269|0.9050|8885.93|
| L |0.8278|KK, degraded|0.6000|0.4232|0.7541|10800.00|

Personal-data pages per year sent abroad under H: 262800

### 2b. Memo (at most 300 words)

To: Head of Operations
Subject: Invoice pipeline: H or L

Accuracy. Overall H scores 87.8 % and L 82.8 %, but the overall figure hides the weak spot: degraded Kazakh scans. There L gets 60 % (95 % interval 42–75 %) and H 80 % (63–91 %). H's weakest cells are tied: degraded Kazakh and degraded Russian, both 24/30. Each cell has only 30 invoices, so intervals are wide and overlap: H's edge is likely but not proven.

Personal data. 16 % of pages carry a name and ИИН: 262,800 pages a year. Law No. 94-V covers the ИИН. Lecture 5.1 questions:
- H: the scan goes to a data centre abroad (known). Who stores it and for how long: unknown; a vendor's statement is not a compliance review
- L: the scan stays on our server in Kazakhstan; we store it and set retention. All three answers are known and checkable

Verifiable safeguards:
- L: written retention period with a deletion log; access list; a test that files are really deleted
- H, if ever used: contract naming country and zero retention; name and ИИН regions blurred before sending, tested on 100 sample pages; independent audit report

Choice. I choose L. It costs $10,800 a year against $8,886 for H, about $1,900 more, and is less accurate. Cost matters less than H's unanswered storage and retention questions

Residual risk: low accuracy on degraded Kazakh scans. Send those, and low-confidence results, to manual review, and re-measure on a larger Kazakh sample. Reconsider H if the safeguards above are met

## Part 3: Explain your own numbers

### Q1

Number: 2.63
Why (at most 40 words): Output tokens cost 6× input tokens, and KK grows only 1.6× in output versus 3.1× in input. Output weighs more in the EN bill, so the cost ratio (2.63) falls below the token ratio (2.96)

### Q2

Number: 447
Why (at most 40 words): Yes. The sentence spans e5 tokens 447–467, inside the 512 limit, so the chunk is retrievable. Only the last ~14 tokens of the chunk are cut, silently: no error appears

### Q3

Number: 43.1
Why (at most 40 words): Top-p cuts the unlikely tail (here Easter) and renormalises the rest; relative odds stay the same. Lower temperature reshapes every probability, sharpening the distribution towards Monday

### Q4

Number: 11
Why (at most 40 words): The public leaderboard prefers X (75 vs 69) because it rewards guessing and never rewards "I don't know". That teaches models to guess and hallucinate. With a wrong-answer penalty, Y wins

### Q5

Number: 13.65
Why (at most 40 words): By this criterion it is over-trained (273 vs 20 tokens per parameter). Chinchilla argued that GPT-3-like models were under-trained: too large for their data, so smaller models with more tokens are better
