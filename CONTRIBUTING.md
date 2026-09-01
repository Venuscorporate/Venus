# Contributing to Venus

Thank you for your interest in contributing to Venus! This document provides guidelines and instructions for contributing.

## Code of Conduct

Please be respectful and constructive in all interactions.

## How to Contribute

### 1. Reporting Issues

Found a bug? Have a suggestion? [Create an issue](https://github.com/Venuscorporate/Venus/issues/new)

**Include:**
- Clear description of the issue
- Steps to reproduce (for bugs)
- Expected vs actual behavior
- Screenshots (if applicable)
- Environment details (OS, Node version, etc.)

### 2. Submitting Changes

1. **Fork the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/Venus.git
   cd Venus
   ```

2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   - Write clean, readable code
   - Follow existing code style
   - Add comments for complex logic
   - Update tests

4. **Test thoroughly**
   ```bash
   npm run test:all
   ```

5. **Commit with clear messages**
   ```bash
   git commit -m "feat: Add your feature description"
   ```

   Format: `type: description`
   - `feat:` New feature
   - `fix:` Bug fix
   - `docs:` Documentation
   - `style:` Code style
   - `refactor:` Code refactoring
   - `test:` Adding tests
   - `chore:` Build, deps, etc.

6. **Push and create Pull Request**
   ```bash
   git push origin feature/your-feature-name
   ```

### 3. Pull Request Guidelines

- Describe what changes you made and why
- Reference related issues: `Closes #123`
- Ensure all tests pass
- Update README/docs if needed
- Keep PRs focused and reasonably sized

## Development Setup

```bash
# Install dependencies
cd frontend && npm install
cd ../backend && npm install

# Start development
npm run dev

# Run tests
npm run test:all
```

## Testing Requirements

- Write tests for new features
- Maintain >80% code coverage
- All tests must pass before merging
- Include both unit and integration tests

## Code Style

- Use consistent naming conventions
- Write descriptive variable/function names
- Add JSDoc comments for functions
- Keep functions small and focused

## Documentation

- Update README for new features
- Add comments for complex logic
- Update API docs if endpoints change
- Keep examples up to date

---

**Thank you for contributing!** 🎉