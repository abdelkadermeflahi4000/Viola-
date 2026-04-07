# Contributing to VIOLA

Thank you for helping build the resonance protocol. Every contribution matters.

## Before You Start

VIOLA is **early research** — not production software. The most valuable contributions right now are:

1. **Solving open research problems** (see below)
2. **Code quality** — tests, documentation, refactoring
3. **Bug reports** — especially in consensus logic

## Open Research Problems (Most Wanted)

These are the hard problems blocking Phase 1. If you have ideas, open an issue immediately.

### 1. Distributed Clock Synchronization
**Problem:** Nodes need nanosecond-precision agreement without a central reference.

Current state: each node uses its own system clock. This is incorrect for a real distributed protocol.

What we need:
- A clock sync algorithm adapted to Schumann-anchored networks
- Analysis of NTP / PTP / logical clocks in this context
- Error bounds for realistic network latency

### 2. Schumann Variance Handling
**Problem:** The Schumann resonance oscillates between 7.2–8.5 Hz due to ionospheric conditions. How do we use it as a reliable timestamp?

Options being considered:
- Rolling median over a time window
- Multiple-harmonic cross-correlation
- Statistical filtering (Kalman?)
- Treating it as a probability distribution, not a point value

### 3. Spam Prevention Without PoW
**Problem:** Without Proof-of-Work fees, what prevents spam?

Proposed: a frequency-based cost model where each message consumes "resonance capacity" proportional to its information content. Not yet specified mathematically.

---

## Code Contributions

### Setup

```bash
git clone https://github.com/viola-protocol/viola
cd viola
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
pip install -r requirements-dev.txt   # testing tools
```

### Running Tests

```bash
pytest tests/ -v
python test_schumann_integration.py
python poc_simulator.py
```

### Code Style

- Python: PEP 8, type hints on all public functions
- Rust: `cargo fmt` before committing
- Comments: explain *why*, not *what*
- Every new algorithm needs a docstring with the equation it implements

### Pull Request Process

1. Fork the repo and create a branch: `git checkout -b feat/your-idea`
2. Write tests for new code
3. Run `pytest tests/` — all tests must pass
4. Open a PR with a clear description of what changed and why
5. Reference any related issues or research papers

### Commit Message Format

```
type(scope): short description

Longer description if needed.

Refs: #123
```

Types: `feat`, `fix`, `docs`, `test`, `refactor`, `perf`, `chore`

---

## Reporting Bugs

Open an issue with:
- Python version and OS
- Full error traceback
- Steps to reproduce
- Expected vs actual behavior

For security vulnerabilities: see [SECURITY.md](SECURITY.md) — do not open a public issue.

---

## Code of Conduct

- Be direct and technical
- Respect that this is research — "I don't know" is a valid answer
- Cite sources for mathematical claims
- No gatekeeping — beginners welcome

---

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

*"If you feel the pulse beneath the protocol, you are already part of the network."*
