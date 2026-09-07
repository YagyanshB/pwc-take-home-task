# TenKay

LLM-based question answering over financial 10-K filings. Compares two OpenAI models on answer quality, abstention, and cost using 50 examples from the Financial Q&A 10-K dataset.

## Project Structure

- `data/` — dataset and selected samples
  - `Financial-QA-10k.csv`
  - `samples_50.csv`
  
- `data/` — predictions and evaluation results
  - `predictions_model_a.csv`
  - `predictions_model_b.csv`
  - `evaluation_summary.csv`
- `financial_qa_evaluation.ipynb` — main notebook
- `.env` 
- `.gitignore`
- `README.md`

## Setup

```bash
git clone https://github.com/YagyanshB/pwc-take-home-task
cd tenkay

python3 -m venv .venv
source .venv/bin/activate

pip install pandas openai python-dotenv tiktoken jupyter ipykernel
Create a .env file in the project root:
```

## Evaluation Principles:
- Exact match after normalisation (preserves $, %, . for financial accuracy)
- LLM-as-a-Judge classifies each prediction as CORRECT, INCORRECT, or ABSTAINED
- Manual review of flagged cases to catch judge errors
- Cost estimation via token counting with tiktoken

## Outputs
All predictions and evaluation results are saved as CSVs in data/ so you can inspect them without rerunning the pipeline.