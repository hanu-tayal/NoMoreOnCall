# Contributing to NoMoreOnCall

Thank you for your interest in contributing! This document provides guidelines for contributing to the project.

## Development Setup

1. Fork and clone the repository
2. Create a virtual environment: `python -m venv .venv`
3. Activate and install: `pip install -r requirements.txt`
4. Run the demo to verify: `python demo.py`

## Adding New Error Types

1. **In `debug_analyzer_v2.py`**: Add mock data for the new error type in `analyze_error()`
2. **In `code_fixer.py`**: Add a new `_fix_*` method in `CodeFixer` and register it in `_generate_fix()`'s `fix_methods` dict

## Code Style

- Use type hints where helpful
- Add docstrings to new functions and classes
- Follow existing patterns in the codebase

## Submitting Changes

1. Create a feature branch from `main`
2. Make your changes with clear commit messages
3. Open a pull request with a description of the change
