# PlanMyTrip: Agentic AI Travel Planner

PlanMyTrip is an agentic AI application that helps users plan their trips by leveraging a modular, tool-augmented workflow. It combines a FastAPI backend (for agentic reasoning and tool orchestration) with a Streamlit frontend (for interactive user experience).

---

## 🧠 Agentic Workflow

The core of PlanMyTrip is an **agentic workflow** built using a graph-based approach. The workflow is orchestrated by the `GraphBuilder` class (`agents/agentic_workflow.py`), which:

- Loads a language model (LLM) and binds it to a set of specialized tools.
- Receives user queries and augments them with a system prompt.
- Uses a graph structure to alternate between agent reasoning and tool invocation, allowing the agent to:
  - Decide when to call tools (e.g., for place search, expense calculation, currency conversion, weather info).
  - Integrate tool outputs into its reasoning loop.
- Returns a final, synthesized answer to the user.

This design enables the agent to break down complex travel planning tasks into smaller, tool-driven steps, providing accurate and actionable travel plans.

---

## 🛠️ Tool Functions

PlanMyTrip uses several modular tools, each encapsulated in the `tools/` directory:

- **Place Search Tool** (`tools/place_search_tool.py`):  
  Searches for attractions, restaurants, activities, and transportation options in a given place using Google Places API and Tavily as a fallback.

- **Expense Calculator Tool** (`tools/expense_calculator_tool.py`):  
  Estimates total hotel costs, calculates total trip expenses, and computes daily expense budgets.

- **Currency Converter Tool** (`tools/currency_converter_tool.py`):  
  Converts amounts between currencies using real-time exchange rates.

- **Weather Info Tool** (`tools/weather_info_tool.py`):  
  Fetches current weather and multi-day forecasts for cities using the OpenWeatherMap API.

Each tool is designed to be invoked by the agent as needed, allowing for flexible and context-aware travel planning.

---

## 🚀 How to Run the Project

### 1. Start the FastAPI Backend

The backend exposes an endpoint for agentic travel planning.  
**Command:**
```bash
uvicorn main:app --reload --port 8000
```
- This will start the FastAPI server on `http://localhost:8000`.
- The `/query` endpoint receives user questions and returns AI-generated travel plans.

### 2. Launch the Streamlit Frontend

The frontend provides a chat-like interface for users to interact with the agent.
**Command:**
```bash
streamlit run app.py
```
- This will open a browser window with the PlanMyTrip UI.
- Enter your travel planning queries and receive detailed, AI-generated itineraries.

---

## 📝 Notes

- **Environment Variables:**  
  Make sure to set the required API keys in your environment (Google Places, OpenWeatherMap, Exchange Rate API, etc.) as referenced in the `.env` file.

- **Extensibility:**  
  The agentic workflow and tool system are modular—new tools can be added easily for additional travel-related functionalities.

---

## 📂 Project Structure

```
agents/
  agentic_workflow.py      # Agentic workflow and graph logic
config/
  config.yaml             # Config file for LLM models
prompts/
  prompt.py               # System prompt for invoking LLM
tools/
  place_search_tool.py     # Place search tool
  expense_calculator_tool.py # Expense calculator tool
  currency_converter_tool.py # Currency converter tool
  weather_info_tool.py     # Weather info tool
utils/
  config_loader.py        # Loads the config.yaml file
  currency_converter.py   # Processes currency conversion
  expense_calculator.py   # Calculates overall travel costs
  model_loader.py         # Loads the LLM
  place_info_search.py    # Searches info using Google Places API
  weather_info.py         # Fetches weather info from OpenWeatherMap API
main.py                   # FastAPI backend
app.py                    # Streamlit frontend
```

---

## 🤖 Example Usage

- "Plan a 5-day trip to Paris with a daily budget of $200."
- "What are the top attractions and restaurants in Tokyo?"
- "Convert 100 USD to EUR for my travel expenses."
- "What's the weather forecast for Rome next week?"

---

*This project demonstrates the power of agentic AI workflows for real-world, tool-augmented applications in travel planning.*
