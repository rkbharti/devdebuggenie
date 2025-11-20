# Contributing to DevDebugGenie

Thank you for considering contributing to DevDebugGenie! This document provides guidelines for contributing to the project.

## How to Contribute

### Reporting Bugs

1. Check if the bug has already been reported in [Issues](https://github.com/rkbharti/devdebuggenie/issues)
2. If not, create a new issue with:
   - Clear title and description
   - Steps to reproduce
   - Expected vs actual behavior
   - Your environment (OS, Python version, etc.)
   - Relevant logs or error messages

### Suggesting Features

1. Check [Discussions](https://github.com/rkbharti/devdebuggenie/discussions) for similar suggestions
2. Create a new discussion with:
   - Clear description of the feature
   - Use cases and benefits
   - Potential implementation approach

### Submitting Code

#### Setup Development Environment

```bash
# Fork and clone the repository
git clone https://github.com/YOUR_USERNAME/devdebuggenie.git
cd devdebuggenie

# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # or .venv\Scripts\activate on Windows

# Install dependencies
pip install -r requirements.txt

# Install development dependencies
pip install black ruff mypy pytest pytest-cov
```

#### Development Workflow

1. **Create a branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes**
   - Write clean, readable code
   - Follow existing code style
   - Add docstrings to functions and classes
   - Update tests if needed

3. **Format and lint**
   ```bash
   black .
   ruff check .
   mypy agents/ tools/
   ```

4. **Run tests**
   ```bash
   pytest
   pytest --cov=agents --cov=tools
   ```

5. **Commit your changes**
   ```bash
   git add .
   git commit -m "feat: Add your feature description"
   ```

   Use conventional commits:
   - `feat:` - New features
   - `fix:` - Bug fixes
   - `docs:` - Documentation changes
   - `test:` - Test additions/changes
   - `refactor:` - Code refactoring
   - `style:` - Code style changes
   - `chore:` - Maintenance tasks

6. **Push and create PR**
   ```bash
   git push origin feature/your-feature-name
   ```
   Then open a Pull Request on GitHub

#### Pull Request Guidelines

- Link related issues in the PR description
- Provide clear description of changes
- Include screenshots/demos for UI changes
- Ensure all tests pass
- Update documentation if needed
- Keep PRs focused and reasonably sized

### Adding New Agents

To add a new specialized agent:

1. **Create agent file** in `agents/` directory:
   ```python
   # agents/your_agent.py
   from google.adk.agents import Agent

   def create_your_agent():
       return Agent(
           model="gemini-2.0-flash-exp",
           name="your_agent_name",
           description="What this agent does",
           instruction="""Detailed instructions for the agent..."""
       )
   ```

2. **Add to coordinator** in `agents/coordinator_agent.py`:
   ```python
   from agents.your_agent import create_your_agent
   
   your_agent = create_your_agent()
   coordinator = Agent(
       ...,
       sub_agents=[..., your_agent]
   )
   ```

3. **Write tests** in `tests/test_agents.py`:
   ```python
   def test_your_agent():
       agent = create_your_agent()
       assert agent.name == "your_agent_name"
   ```

4. **Update documentation**:
   - Add agent description to README.md
   - Update architecture diagram
   - Add usage examples

### Code Style

- Follow PEP 8 guidelines
- Use type hints for function parameters and return values
- Write docstrings for all public functions and classes
- Keep functions small and focused
- Use meaningful variable names
- Add comments for complex logic

### Testing

- Write unit tests for new functionality
- Ensure test coverage doesn't decrease
- Test edge cases and error conditions
- Use pytest fixtures for common setup

### Documentation

- Update README.md for user-facing changes
- Update docstrings for code changes
- Add examples for new features
- Keep ARCHITECTURE.md in sync with code structure

## Community Guidelines

- Be respectful and inclusive
- Help others learn and grow
- Provide constructive feedback
- Focus on the issue, not the person
- Follow the [Code of Conduct](CODE_OF_CONDUCT.md)

## Questions?

Feel free to ask in:
- [GitHub Discussions](https://github.com/rkbharti/devdebuggenie/discussions)
- [Issues](https://github.com/rkbharti/devdebuggenie/issues) (for bugs)

## Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Appreciated in the community!

Thank you for making DevDebugGenie better! 🚀