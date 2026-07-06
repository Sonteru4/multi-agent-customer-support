# Multi-Agent Customer Support Bot

Streamlit chat interface connected to a multi-agent Langflow workflow for customer support queries.

## Overview

This project provides a Streamlit web UI that sends user messages to a hosted Langflow API and displays agent responses in a chat history panel. The Langflow flow (`Customer Support Langflow.json`) defines a multi-agent architecture: a routing agent delegates to specialized sub-agents for FAQ lookup, order lookup, and product lookup via AstraDB tools. Sample CSV files for products and orders are included as reference data for the flow. The Streamlit app handles message input, API calls, response parsing, and session-based chat history.

## Tech Stack

- Python
- Streamlit
- Langflow (hosted on Astra DataStax)
- requests
- python-dotenv

## Features

- Streamlit two-column UI: message input on the left, chat history on the right
- Calls Langflow run API endpoint (`/api/v1/run/customer`) with chat input/output
- Session-state chat history persisted across interactions within a session
- Langflow flow with three Agent nodes:
  - FAQ agent — answers frequently asked questions
  - Order/product agent — looks up orders and aggregates product details via AstraDB tools
  - Router agent — routes user inquiries to the appropriate sub-agent tools
- Sample data files: `Sample Products.csv`, `Sample Orders.csv`
- Exportable Langflow flow definition in `Customer Support Langflow.json`

## Getting Started

1. Install dependencies:

```bash
pip install -r requirements.txt
```

2. Create a `.env` file with your Langflow API credentials:

```
APPLICATION_TOKEN=your_langflow_application_token
```

Additional Langflow configuration (API URL, flow ID, endpoint name) is defined as constants in `main.py` (`BASE_API_URL`, `LANGFLOW_ID`, `FLOW_ID`, `ENDPOINT`).

3. Import the Langflow flow (if running your own Langflow instance):

- Open Langflow and import `Customer Support Langflow.json`
- Configure AstraDB tools and upload sample CSV/PDF data as referenced in the flow
- Update the constants in `main.py` to match your deployment

4. Run the Streamlit app:

```bash
streamlit run main.py
```

The app opens in your browser at `http://localhost:8501`.

## Project Structure

```
Multi-agent-customer-support-bot/
├── main.py                          # Streamlit UI and Langflow API client
├── requirements.txt                 # Python dependencies
├── Customer Support Langflow.json   # Langflow multi-agent flow export
├── Sample Products.csv              # Sample product catalog
└── Sample Orders.csv                # Sample order records
```
