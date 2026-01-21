# Contributing to AI Tech Collective

Thank you for your interest in contributing! This project welcomes contributions from the community.

## How to Contribute

### 🐛 Report Bugs

Found a bug? Help us fix it:

1. Check [existing issues](https://github.com/cbolden15/ai-tech-collective/issues) first
2. If new, [open an issue](https://github.com/cbolden15/ai-tech-collective/issues/new)
3. Include:
   - Clear description
   - Steps to reproduce
   - Expected vs actual behavior
   - n8n version
   - Error messages/logs

### 💡 Suggest Enhancements

Have an idea? We'd love to hear it:

1. [Open an issue](https://github.com/cbolden15/ai-tech-collective/issues/new)
2. Label it as "enhancement"
3. Describe:
   - The problem it solves
   - Your proposed solution
   - Why it's valuable

### 🔧 Submit Pull Requests

Ready to code?

1. **Fork the repository**
2. **Create a branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes**
4. **Test thoroughly**
5. **Commit with clear messages**
   ```bash
   git commit -m "Add: feature description"
   ```
6. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```
7. **Open a Pull Request**

### 📝 Improve Documentation

Documentation contributions are highly valued:

- Fix typos or unclear explanations
- Add examples
- Improve setup instructions
- Translate to other languages

## Contribution Ideas

### Easy (Good First Issue)

- Add more AI news sources
- Improve error messages
- Add workflow validation
- Create setup videos/screenshots

### Medium

- Add new output formats (Twitter threads, LinkedIn posts)
- Implement multi-language support
- Create analytics dashboard
- Add email delivery option

### Advanced

- Build web UI for configuration
- Add caching to reduce API costs
- Implement incremental updates
- Create workflow templates for other industries

## Code Style

### Workflow JSON

- Use clear, descriptive node names
- Add comments in Code nodes
- Keep expressions readable
- Test all branches

### Documentation

- Use clear, concise language
- Include code examples
- Add screenshots when helpful
- Test all instructions

### Commit Messages

Format: `Type: Description`

**Types:**
- `Add:` New feature
- `Fix:` Bug fix
- `Update:` Modify existing feature
- `Docs:` Documentation only
- `Refactor:` Code cleanup

**Examples:**
- `Add: LinkedIn post generation node`
- `Fix: Base64 encoding for Unicode characters`
- `Update: Gemini API to 2.5 Flash`
- `Docs: Clarify GitHub token permissions`

## Security

### Reporting Security Issues

**DO NOT** open public issues for security vulnerabilities.

Instead:
1. Email: [your-email]
2. Include:
   - Description of vulnerability
   - Steps to reproduce
   - Potential impact

### Secrets Management

**Never commit:**
- API keys
- Tokens
- Webhook URLs
- Credentials
- Private information

**Always:**
- Use placeholders in examples
- Check `.gitignore` is working
- Review changes before committing
- Use environment variables

## Testing

### Before Submitting

1. **Test the workflow**
   - Import in clean n8n instance
   - Verify all nodes execute
   - Check outputs are correct

2. **Test documentation**
   - Follow your own instructions
   - Verify all links work
   - Check code examples run

3. **Review changes**
   - No secrets committed
   - Code is clean
   - Documentation is clear

## Review Process

### What to Expect

1. **Initial review** within 48 hours
2. **Feedback** if changes needed
3. **Approval** and merge when ready

### Review Criteria

- ✅ Works as described
- ✅ No secrets exposed
- ✅ Documentation updated
- ✅ Follows code style
- ✅ Tests pass

## Community Guidelines

### Be Respectful

- Treat everyone with respect
- Welcome newcomers
- Provide constructive feedback
- Celebrate contributions

### Be Collaborative

- Help others succeed
- Share knowledge
- Ask questions
- Learn together

### Be Professional

- Focus on the work
- Accept feedback gracefully
- Admit mistakes
- Keep improving

## Recognition

### Contributors

All contributors are recognized in:
- GitHub contributor list
- Release notes
- Project documentation

### Maintainers

Active, consistent contributors may be invited to become maintainers.

## Questions?

- **General questions**: [Open a discussion](https://github.com/cbolden15/ai-tech-collective/discussions)
- **Setup help**: See [SETUP.md](docs/SETUP.md)
- **Bugs**: [Open an issue](https://github.com/cbolden15/ai-tech-collective/issues)

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for contributing to AI Tech Collective! 🚀**

Every contribution, no matter how small, helps make this project better for everyone.
