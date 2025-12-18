README – AI Model Release Trends Analysis (Hugging Face)
Project Title

Analysis of AI Model Release Trends Using Hugging Face Metadata


Research Methods – 2025

Group Members:

Vanessa Pemba

Clive Chinkhuntha

Annette Ching'amba

Taonga Kamanga

Prisca Mtengowaminga

Chisomo Kawanga

Submission Date:  19/12/2025


1. Project Overview

This project investigates trends in Artificial Intelligence (AI) model releases across four major categories: Text, Vision, Audio, and Multimodal. Using publicly available metadata from the Hugging Face platform, the study analyses model release frequency, downloads, likes, and trending scores. The objective is to understand how recent advances in Large Language Models (LLMs) and generative AI technologies are shaping current AI research and development trends.


2. Research Question and Hypothesis
Research Question

Which types of AI models are released most frequently (Text, Vision, Audio), and what does this indicate about current AI research trends?

Hypothesis

Model releases in the Text category have increased sharply in the this year(2025) due to rapid advancements in LLMs and generative AI.


3. Data Source

Platform: Hugging Face

API Endpoint: https://huggingface.co/api/models

Access Type: Public (no authentication required)

Data Format: Structured JSON

Data Type: Quantitative

Collected Fields

Model name

Category (pipeline_tag: text, vision, audio, multimodal)

Year (derived from createdAt)

Downloads

Likes

Trending score


4. Tools and Technologies
Programming Language

Python 3.10 or higher


Environment

Jupyter Notebook


Libraries Used

pandas

requests

matplotlib

seaborn

numpy


5. Project Folder Structure
data_generation/
│
├── ict.ipynb              # Main Jupyter Notebook             
├── cleaned_model_data.csv # Cleaned and validated dataset
├── metadata.json          # Dataset metadata
├── figures/               # Generated visualisations
│   ├── downloads_by_category.png
│   ├── likes_by_category.png
│   ├── trendingScores_by_category.png
│   ├── category_distribution.png
│   └── Year_pie.png
└── README.md              # Project documentation


6. Steps to Reproduce the Dataset and Analysis
Step 1: Install Python

Ensure Python version 3.10 or higher is installed.

Check the version:

python --version

Step 2: Create and Activate a Virtual Environment (Recommended)

Create the environment:

python -m venv venv


Activate:

Windows

venv\Scripts\activate


Linux / macOS

source venv/bin/activate

Step 3: Install Required Libraries
pip install pandas requests matplotlib seaborn numpy

Step 4: Launch Jupyter Notebook
jupyter notebook


Open the notebook file:

ict.ipynb

Step 5: Execute Notebook Cells Sequentially

Run all cells from top to bottom in the following order:

Import libraries

Retrieve data from the Hugging Face API

Save raw data to models.csv

Clean and preprocess the dataset

Generate visualisations

Export the cleaned dataset

⚠️ Important: Skipping cells may cause errors or missing outputs.


7. Data Cleaning and Validation
Cleaning Procedures

Removed records with missing category or year

Converted timestamps to year format

Removed duplicate model entries

Ensured numeric values (downloads, likes, trending score) were valid and non-negative

Validation Checks

Verified category distributions

Checked yearly release trends

Compared summary statistics before and after cleaning


8. Data Analysis and Visualisation
Visualisations Produced

Bar Charts

Category vs Downloads

Category vs Likes

Category vs Trending Score

Pie Chart

Distribution of models released per year

Interpretation

The analysis shows that Text-based models dominate in both release frequency and popularity metrics. This strongly supports the hypothesis that LLM-focused research is the primary driver of recent AI development trends.


9. Reproducibility Notes

All data was obtained from a public API

No random seeds were required (deterministic data)

Full analysis can be reproduced using the provided notebook

No sensitive or personal data was collected


10. Ethical and Privacy Considerations

All data is publicly available

No personal or user-level information collected

Minimal privacy risk

Complies with Hugging Face terms of service


11. Expected Outputs

After successful execution, the following files should be generated:

models.csv

cleaned_models.csv

Four visualisation images stored in /figures

Updated metadata.json


12. Contact / Maintainer

Project Maintained By:
Research Methods Group 6 
Mzuzu University
Department of ICT