# Email Triage Environment for AI Agents

This project implements a **real‑world email triage environment** using the OpenEnv framework. It contains three tasks of increasing difficulty, each with a programmatic grader and a reward function that provides partial feedback. A baseline inference script uses an LLM via the OpenAI API to solve the tasks.

## Tasks

1. **Spam Detection (Easy)**  
   Classify an email as spam or ham.  
   *Reward:* 1.0 for correct, 0.0 otherwise.

2. **Priority Classification (Medium)**  
   Assign a priority: high, medium, or low.  
   *Reward:* 1.0 for exact match, 0.5 for adjacent (e.g., high vs medium), 0.0 otherwise.

3. **Response Drafting (Hard)**  
   Write a professional reply to an email.  
   *Reward:* weighted combination of keyword coverage (70%) and politeness (30%).

## OpenEnv Compliance

The environment (`EmailTriageEnv`) implements the full OpenEnv interface:
- `reset(task_id, email_index) → EmailObservation`
- `step(action) → (observation, reward, done, info)`
- `state() → dict`

All data models are defined with Pydantic (`EmailObservation`, `EmailAction`).

## Usage

### Environment Variables
Before running, set:
- `API_BASE_URL` – The LLM endpoint (e.g., `https://api.openai.com/v1`)
- `MODEL_NAME` – The model identifier (e.g., `gpt-3.5-turbo`)
- `HF_TOKEN` – Your API key

### Run Locally
```bash
pip install -r requirements.txt
export API_BASE_URL=...
export MODEL_NAME=...
export HF_TOKEN=...
python inference.py
