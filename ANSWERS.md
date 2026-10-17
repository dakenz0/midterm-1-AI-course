# Midterm 1: answers

GitHub username: dakenz0
Session code: kettle-62
Fingerprint: 2f8a328a

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

I worked on this assignment with help from Codex. I used it for calculations, checking results and discussing the three parts. Codex used Python to calculate and check recall, MRR, Wilson intervals and costs. It also helped draft the written answers.
The assistant helped me compare the options and explain the reasons for choosing them. I asked questions about ranks, recall and the decision in Part 1. Codex explained these ideas and checked the results using the given formulas.
The AI help included calculations, explanations and writing. I am responsible for the final answers and must be able to explain the numbers and decisions during the oral check.

(About half a page: which assistants or tools you used and for what. If you used none, say so.)

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A | 0.450000 | 0.616667 | 0.733333 | 0.544484 |
| B | 0.216667 | 0.366667 | 0.433333 | 0.327222

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 | 0.616667 | 0.490174 | 0.729119 |
| A, k=5 | 0.733333 | 0.609910 | 0.828675 |
| B, k=3 | 0.366667 | 0.256207 | 0.493172 |
| B, k=5 | 0.433333 | 0.315722 | 0.558968

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 | 14074.60 |
| A, k=5 | 18087.74 |
| B, k=3 | 9627.37 |
| B, k=5 | 10675.68

### 1d. Decision (at most 150 words)


Chosen candidate: B, k=3
I choose B, k=3. Its yearly cost is 9627.37 USD, below the 12400 budget. Recall is 22/60 = 36.67%, with Wilson interval [25.62%, 49.32%]. B, k=5 has 43.33% recall [31.57%, 55.90%] and costs 10675.68. Their intervals overlap, so under the course rule this test does not show a winner. This does not prove equal quality. B, k=3 saves 1048.31 USD per year. Both A options are over budget: A, k=3 costs 14074.60; A, k=5 costs 18087.74. A, k=5 has interval [60.99%, 82.87%], above both B intervals without overlap, but it costs too much. My choice has recall EN 8/20 = 40%, RU 8/20 = 40%, and KK 6/20 = 30%. KK has the lowest recall here. The language groups are small, so we need more tests.

### 1e. Next measurement (at most 60 words) 
Test B, k=3 and B, k=5 on the same 600 new questions: 200 per language, like real customer questions. Compare overall and language recall with Wilson intervals. If B, k=5 shows a clear improvement, especially for KK, its extra 1048.31 USD per year may be worth paying within budget.
## Part 2: A document pipeline you can defend


### 2a. Numbers

| pipeline| overall accuracy | weakest cell (language, condition) | accuracy there | lower   | upper   | annual cost |
|---------|------------------|------------------------------------|----------------|---------|---------|-------------|
| H       | 0.883333         | RU, degraded                       | 0.733333       | 0.555517| 0.858175| 9083.03     | 
| L       | 0.816667         | RU, degraded                       | 0.700000       | 0.521239| 0.833354| 5400.00     |

Personal-data pages per year sent abroad under H: 140525

### 2b. Memo (at most 300 words)
To: Head of Operations

I choose L. Before use, we need a legal review and a person must check each invoice. H costs 17187.85 USD per year; L costs 27000. H gets 152/180 invoices right (84.44%); L gets 147/180 (81.67%). Their overall Wilson intervals overlap: H [78.44%, 89.01%], L [75.37%, 86.64%]. This test does not show a clear accuracy winner.
H works worst for KK, clean scans. L works worst for KK, degraded scans. Both get 22/30 right (73.33%), with 95% Wilson interval [55.55%, 85.82%]. These wide intervals mean we need more tests to check which groups are weakest. The overall results hide these weaker groups.
With H, scans go abroad, including 434350 pages with personal data each year. We must find the exact country, who can read or store the data, and how long they keep it. This includes other companies, logs and backup copies. Names and IIN need a legal review. The service provider's promise is not enough.
L processes scans on bank servers in Kazakhstan. We must check where all copies and backups go, who has access, and how long files stay. Local storage alone does not prove that the bank follows the law. L needs three servers at 750 USD per month each.
Encrypt stored and sent data. Limit staff access and use two-step login. Keep access logs without invoice contents. Block outside data sharing and check network logs. I propose a 30-day storage limit for source images. Test deletion, including backups. Check all four fields and review results by language and scan condition.
L gives the bank more control, but costs more. Remaining risks include Kazakh extraction errors, human mistakes and staff misuse of access. Human checks and data protection cost extra.

## Part 3: Explain your own numbers

### Q1

Number: 2.20 (bill ratio); total-token ratio = 2.43
Why (at most 40 words): An output token costs six times as much as an input token. English has a higher share of output tokens. This makes the bill ratio lower than the ratio of all tokens (2.43)

### Q2

Number: 44.4%
Why (at most 40 words): Only English is cut: EN has 920.5 e5 tokens, RU 448 and KK 266. English's last 408.5 tokens are left out without an error message. The embedding does not represent this part, so search loses its information

### Q3

Number: 81.2 %
Why (at most 40 words): Lowering temperature to 0.5 does not change the token order. It makes Monday more likely. All five tokens can still be chosen: positive temperature changes their probabilities but does not remove tokens

### Q4

Number: 28.7 %
Why (at most 40 words): For a calibrated base model, the course rule uses account numbers and birthdays. I leave out multiplication and sequences because they follow rules. 'Never invent' adds no missing facts and cannot remove this limit by itself

### Q5

Number: 6.00
Why (at most 40 words): The model has 120 tokens per parameter; Chinchilla has 20. It is over-trained by this compute rule. This does not mean overfitting. Chinchilla said models like GPT-3 needed more training data for their size
