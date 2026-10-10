# CrewAI + Gemini Agent Fundamentals

This project contains a beginner-friendly Jupyter notebook that demonstrates the core CrewAI workflow:

`LLM -> Agent -> Task -> Crew`

## Prerequisites

- Windows with PowerShell
- Python 3.10 or newer
- A Gemini API key from Google AI Studio
- Visual Studio Code with the Python and Jupyter extensions

## 1. Open the project folder

Open PowerShell and move to the project directory:

```powershell
cd "Enter project path"
```

## 2. Check Python

Confirm that the Python launcher is installed:

```powershell
py --version
```

List the Python installations detected by the launcher:

```powershell
py -0p
```

Python 3.10 or newer is required. If `py` is not recognized, install Python from [python.org](https://www.python.org/downloads/) and enable **Add Python to PATH** during installation.

## 3. Create the virtual environment

Run this command once from the project directory:

```powershell
py -m venv .venv
```

Confirm that the environment was created:

```powershell
Test-Path .\.venv\Scripts\python.exe
```

The command should return `True`.

## 4. Activate the virtual environment

```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks the activation script, allow local scripts for the current terminal session and try again:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
.\.venv\Scripts\Activate.ps1
```

The PowerShell prompt should now begin with `(.venv)`.

Verify that the active Python executable belongs to this project:

```powershell
python --version
python -c "import sys; print(sys.executable)"
python -m pip --version
```

The executable path should end with:

```text
CrewAIAgent\.venv\Scripts\python.exe
```

## 5. Install the dependencies

Upgrade `pip`, then install the packages required by the notebook:

```powershell
python -m pip install --upgrade pip
python -m pip install crewai python-dotenv jupyter ipykernel
```

Check that the main packages import successfully:

```powershell
python -c "import crewai, dotenv; print('CrewAI:', crewai.__version__)"
```

## 6. Configure the Gemini API key

Create a `.env` file in the project directory:

```powershell
New-Item -ItemType File -Path .env -Force
```

Add the following line to `.env`, replacing the placeholder with your Gemini API key:

```dotenv
GEMINI_API_KEY=your_gemini_api_key_here
```


```powershell
python -c "from dotenv import load_dotenv; import os; load_dotenv(); print('Gemini key configured:', bool(os.getenv('GEMINI_API_KEY')))"
```

The command should print:

```text
Gemini key configured: True
```

## 7. Register the Jupyter kernel

Register the virtual environment as a notebook kernel:

```powershell
python -m ipykernel install --user --name crewaiagent --display-name "Python (CrewAIAgent)"
```

Confirm that the kernel is available:

```powershell
jupyter kernelspec list
```

The output should include `crewaiagent`.

## 8. Open and run the notebook

Open `CrewAI_Gemini_Agent_Fundamentals.ipynb` in Visual Studio Code.

1. Select **Python (CrewAIAgent)** from the kernel picker in the upper-right corner.
2. Run the environment verification cell first.
3. Confirm that the displayed Python executable points to `.venv`.
4. In the Gemini configuration cell, set `model` to a Gemini model available to your Google AI Studio project.
5. Run the remaining cells in order.

The notebook uses the asynchronous CrewAI API because Jupyter already runs an event loop:

```python
result = await gemini_crew.kickoff_async()
```

## Start a later session

Each time you open a new PowerShell terminal, reactivate the environment before running the notebook:

```powershell
cd "Enter your project Path"
.\.venv\Scripts\Activate.ps1
```

Then verify the active interpreter:

```powershell
python -c "import sys; print(sys.executable)"
```

## Deactivate the environment

When finished, run:

```powershell
deactivate
```
