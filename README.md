# Financial Q&A 10-K — LLM Evaluation

A lightweight LLM-based question-answering pipeline for evaluating financial questions using context from company 10-K filings.

The project compares two LLMs on exactly 50 examples from the Financial Q&A 10-K dataset and evaluates their answer quality, abstention behaviour, and estimated cost.

Project Structure
financial-qa-llm-evaluation/
│
├── data/
│   ├── Financial-QA-10k.csv
│   └── samples_50.csv
│
├── outputs/
│   ├── model_a_final_results.csv
│   ├── model_b_final_results.csv
│   └── final_model_comparison.csv
│
├── financial_qa_evaluation.ipynb
├── .gitignore
└── README.md

Requirements
Python 3.12+
An OpenAI API key
Internet connection for API requests

The pipeline uses the supplied dataset context only. It does not use RAG, external retrieval, or MCP servers.

Setup
1. Clone the repository
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd financial-qa-llm-evaluation

2. Create a virtual environment
python3 -m venv .venv
source .venv/bin/activate


On Windows:

.venv\Scripts\activate

3. Install dependencies
pip install pandas openai python-dotenv tiktoken jupyter ipykernel

4. Configure the OpenAI API key

Create a file named .env in the project root:

OPENAI_API_KEY=your_api_key_here


Do not commit the .env file to GitHub.

The repository's .gitignore excludes .env and the virtual environment.

Dataset

The project uses the Financial Q&A 10-K dataset from Kaggle:

https://www.kaggle.com/datasets/yousefsaeedian/financial-q-and-a-10k

Place the downloaded CSV in the data/ directory.

The notebook selects exactly 50 valid samples for evaluation.

Running the Evaluation

Start Jupyter:

jupyter notebook


or:

jupyter lab


Open:

financial_qa_evaluation.ipynb


Run the notebook cells from top to bottom.

The notebook will:

Load and validate the dataset.
Select exactly 50 samples.
Construct prompts containing only the question and supplied context.
Generate answers using two candidate LLMs.
Record whether a model abstains.
Evaluate predictions against the reference answers.
Manually validate cases flagged by the automated evaluator.
Produce comparison and cost results.
Save structured outputs to the outputs/ directory.
Evaluation Approach

The evaluation focuses on:

Answer correctness
Semantic equivalence with the reference answer
Appropriate abstention when the context is insufficient
Coverage
Model agreement
Estimated inference cost

An LLM-based evaluator is used for the initial assessment. Cases flagged as incorrect or requiring further review are manually checked to reduce the risk of incorrectly penalising answers that are semantically correct but phrased differently from the reference answer.

Important Design Constraint

The models are instructed to answer only from the provided context.

No external financial knowledge, web search, RAG, vector database, or MCP server is used when generating answers.

This ensures that the evaluation measures the models' ability to answer questions using the supplied 10-K context.

Outputs

The notebook produces structured CSV files containing model predictions and evaluation results.

Examples include:

outputs/model_a_final_results.csv
outputs/model_b_final_results.csv
outputs/final_model_comparison.csv


These files can be used for further analysis without rerunning the model evaluation.

Production Considerations

The evaluation contains only 50 examples and should therefore be treated as an initial model comparison rather than a production certification.

A production evaluation should use a larger and more representative dataset and should include:

Difficult numerical questions
Ambiguous questions
Unsupported questions requiring abstention
Different companies and filing types
Accuracy and reliability measurements
Latency and throughput
Actual inference cost

Where models demonstrate comparable quality and reliability, the lower-cost model may be preferable for production deployment.

Reproducibility

The evaluation uses a fixed set of 50 samples and a consistent prompt structure so that the experiment can be reproduced.

API-based LLM outputs may vary between runs depending on model behaviour and API configuration.

Security

Never commit your OpenAI API key.

The following files/directories should remain local:

.env
.venv/
