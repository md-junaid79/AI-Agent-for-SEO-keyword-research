# ✨ AI-Agent-for-SEO-keyword-research
Keyword research AI Agent that takes 1 seed keyword as an input (e.g. nvidia) and suggest 50 keyword candidates that are sorted by the least competition and most monthly search volume. The suggested keywords are the ones that we can target to show up as the first page of Google search thereby reducing manual efforts for SEO keyword reaserach.


##  📈Project Overview

The **SEO Keyword  Agent** is a powerful automation tool designed to eliminate manual keyword research by identifying the **Top 50 high-value, low-competition keyword opportunities** from a single seed word.

This agent transforms thousands of raw suggestions into a prioritized, production-ready list in **under 4 seconds per query**, making keyword strategy fast, objective, and data-driven.

---

## 🎯 The Core Logic: Opportunity Score

The agent's intelligence lies in its proprietary scoring mechanism and filtering process, which is designed to identify "money keywords" that are easy to rank for.

### The Formula:

The Opportunity Score prioritizes keywords with high traffic potential (Volume) and high commercial intent (CPC).

$$\text{Opportunity Score} = (\text{Search Volume} \times \text{Cost Per Click (CPC)}$$ ) / Competition

### The Filtering Process:

After scoring all candidates, a conditional filter removes "bad" keywords that do not meet minimum profitability or rankability thresholds (as executed in the 'Filter out bad keywords' step).

| Criteria | Rule | Rationale |
| :--- | :--- | :--- |
| **High Competition** | **REMOVE** if competition is high (e.g., competition score $\gt 0.75$). | Focuses on easy-to-rank terms. |
| **Low Volume** | **REMOVE** if Search Volume $\lt 100$. | Ensures minimum traffic potential. |
| **Non-Commercial** | **REMOVE** if CPC is $\$0$. | Discards purely informational keywords that hold little direct revenue potential. |

---

## ⚙️ Workflow Architecture and Pipeline

The agent executes a streamlined, 7-step data processing pipeline (The Funnel) to transform the initial input into the final output.

The diagram below illustrates how a large set of keywords (e.g., **1,654 items**) is systematically refined down to the **50 most valuable opportunities**.
<p align="center">
  <img src="Screenshot 2025-10-19 161730.png" alt="WORKFLOW FLOW" width="550"/>
</p>

| Step | Component / Action | Function | Data In / Out (Example) |
| :--- | :--- | :--- | :--- |
| **1. Seed Keyword Input** | User Input | Triggers the workflow with one initial keyword. | 1 item |
| **2. HTTP Keyword Suggestions** | **DataForSEO API Call** | Fetches raw related suggestions, volume, CPC, and competition data. | 1 item |
| **3. Extract Suggestions** | Data Parsing | Parses the raw API JSON response into a clean array of keyword objects. | 1,654 items |
| **4. Calculate Opportunity Score** | **Core Logic** | Applies the $\text{Volume} \times \text{CPC}$ formula to every keyword. | 1,654 items |
| **5. Append All Rows to Sheets** | Google Sheets Action | Writes the *full* set of scored keywords to a sheet for auditing. | 1,654 items |
| **6. Filter Bad Results** | **Conditional Split** | Filters out keywords based on Competition and Volume thresholds. | Reduced to 626 items (Pass) |
| **7. Fetch Top 50 Opportunities** | Final Selection | Sorts the filtered list by **Opportunity Score (DESC)** and extracts the top 50. | 50 items |
| **8. Append in top 50 sheet** | Google Sheets Action | Appends the final, actionable list to the result sheet. | 50 items |


---


##  **Deploy the Workflow:**
    Import the workflow definition file (e.g., `workflow.json` or equivalent platform file) into your chosen automation platform.
##   **Execute:**
    Provide a seed keyword to the initial node (Step 1) and run the workflow. The final results will appear in your Google Sheet!
