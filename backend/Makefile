.PHONY: install test lint format run help

# Variables
PYTHON := python
VENV := venv

# Detect OS and check if venv exists
ifeq ($(OS),Windows_NT)
    VENV_EXISTS := $(wildcard $(VENV)/Scripts/pip.exe)
    ifeq ($(VENV_EXISTS),)
        # No venv, use system Python
        PIP := pip
        PYTEST := pytest
        BLACK := black
        FLAKE8 := flake8
        MYPY := mypy
        UVICORN := uvicorn
    else
        # Use venv
        PIP := $(VENV)/Scripts/pip
        PYTEST := $(VENV)/Scripts/pytest
        BLACK := $(VENV)/Scripts/black
        FLAKE8 := $(VENV)/Scripts/flake8
        MYPY := $(VENV)/Scripts/mypy
        UVICORN := $(VENV)/Scripts/uvicorn
    endif
else
    VENV_EXISTS := $(wildcard $(VENV)/bin/pip)
    ifeq ($(VENV_EXISTS),)
        # No venv, use system Python
        PIP := pip
        PYTEST := pytest
        BLACK := black
        FLAKE8 := flake8
        MYPY := mypy
        UVICORN := uvicorn
    else
        # Use venv
        PIP := $(VENV)/bin/pip
        PYTEST := $(VENV)/bin/pytest
        BLACK := $(VENV)/bin/black
        FLAKE8 := $(VENV)/bin/flake8
        MYPY := $(VENV)/bin/mypy
        UVICORN := $(VENV)/bin/uvicorn
    endif
endif

help:
	@echo "Available commands:"
	@echo "  make install  - Create virtual environment and install dependencies"
	@echo "  make test     - Run tests with pytest"
	@echo "  make lint     - Run linting checks (flake8, mypy)"
	@echo "  make format   - Format code with black"
	@echo "  make run      - Run the FastAPI application"

install:
	@echo "Creating virtual environment..."
	$(PYTHON) -m venv $(VENV)
	@echo "Installing dependencies..."
	$(PIP) install --upgrade pip
	$(PIP) install -r requirements.txt
	@echo "Installation complete!"

test:
	@echo "Running tests..."
	$(PYTEST) tests/ -v --cov=src --cov-report=html --cov-report=term

lint:
	@echo "Running flake8..."
	$(FLAKE8) src/ tests/ --max-line-length=100 --exclude=venv,__pycache__
	@echo "Running mypy..."
	$(MYPY) src/ --ignore-missing-imports

format:
	@echo "Formatting code with black..."
	$(BLACK) src/ tests/

run:
	@echo "Starting FastAPI application..."
	$(UVICORN) src.presentation.main:app --reload --host 0.0.0.0 --port 8000

