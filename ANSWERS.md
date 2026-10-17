# Midterm 1: answers

GitHub username: dakenz0
Session code: practice
Fingerprint: 62355e0a

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
| A | 0.733333 | 0.800000 | 0.850000 | 0.780317 |
| B | 0.283333 | 0.433333 | 0.733333 | 0.417381

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 | 0.800000 | 0.682180 | 0.881716 |
| A, k=5 | 0.850000 | 0.738852 | 0.919027 |
| B, k=3 | 0.433333 | 0.315722 | 0.558968 |
| B, k=5 | 0.733333 | 0.609910 | 0.828675

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 | 15291.28 |
| A, k=5 | 20432.17 |
| B, k=3 | 9660.92 |
| B, k=5 | 11048.24

### 1d. Decision (at most 150 words)


Chosen candidate: B, k=5
I  choose B, k=5. It costs 11048.24 USD per year, below the 17900 budget. Its recall is 44/60 = 73.33%, with Wilson interval [60.99%, 82.87%]. A, k=3 has 80.00% recall [68.22%, 88.17%]. The intervals overlap, so this test does not show that A is better under the course rule. This does not mean equal quality. B, k=5 saves 4243.04 USD per year. A, k=5 costs 20432.17, above budget. B, k=3 costs less, but its interval [31.57%, 55.90%] is below B, k=5 without overlap. This supports B, k=5 over B, k=3. For my choice, recall is EN 70% (14/20), RU 70% (14/20), and KK 80% (16/20). EN and RU have the lowest recall here. With only 20 questions per language, we need more tests.

### 1e. Next measurement (at most 60 words)
Test A, k=3 and B, k=5 on the same 600 new questions: 200 per language, like real customer questions. Calculate recall and Wilson intervals for each language and overall. If A shows clearly higher recall, its extra 4243.04 USD per year may be worth paying within budget. Otherwise, keep B, k=5.
## Part 2: A document pipeline you can defend


### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | | | | | | |
| L | | | | | | |

Personal-data pages per year sent abroad under H:

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

Number: 2.17 (bill ratio); total-token ratio = 2.24.
Why (at most 40 words): An output token costs five times as much as an input token. English has a higher share of output tokens. So the cost ratio is lower than the ratio of all tokens (2.24).

### Q2

Number: 355
Why (at most 40 words): Yes. The sentence starts near token 355 and ends before token 512. Its words can help find the chunk, but success is not certain. The later part is cut off without an error message.

### Q3

Number: 54.2 %
Why (at most 40 words): Top-p keeps the most likely tokens until their probabilities add up to at least 0.9. It removes the rest and makes the remaining probabilities add to 1. Lower temperature makes likely tokens more likely but keeps all tokens.

### Q4

Number: 21.2 %
Why (at most 40 words): For a base model with calibrated probabilities, we use account numbers and birthdays. We leave out multiplication and number sequences because they follow rules. A prompt adds no missing facts and cannot guarantee removing this limit.

### Q5

Number: 60494
Why (at most 40 words): The first message is sent in all 28 requests. Prompt caching can make repeated text cheaper to process. The model still needs the chat history in each request and does not get a permanent memory.
