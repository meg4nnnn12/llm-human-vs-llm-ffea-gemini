# Reproduction Report: LLM Style Mirroring Experiment

**Author:** Megan Cheng  
**Date:** January 29, 2026  
**Original Project:** https://github.com/Hypogenic-AI/llm-human-vs-llm-ffea-gemini

## 1. Overview

This report documents my reproduction of the LLM style mirroring experiment, which investigates whether Large Language Models respond differently when prompted by humans versus AI-generated prompts.

## 2. What I Reproduced

The original repository already contained the complete experiment results (`experiment_results.json`, `paired_prompts.json`), so I focused on reproducing the **analysis phase** of the research.

## 3. Setup Process

### Environment
- **OS:** macOS (Apple Silicon)
- **Python Version:** 3.11.2
- **Installation Method:** System Python with pip

### Dependencies Installed
I manually installed the following packages (the original `requirements.txt` had some issues):
```bash
python3 -m pip install openai tqdm anthropic matplotlib scipy numpy pandas seaborn tenacity textblob --break-system-packages
```

### Challenges Encountered

1. **Broken requirements.txt**: The file contained an invalid Anaconda path reference
   - **Solution:** Manually identified and installed required packages

2. **Missing packages**: Several packages weren't listed but were needed
   - **Solution:** Installed them as errors appeared (tenacity, textblob)

3. **Virtual environment issues**: The `uv venv` approach had problems
   - **Solution:** Used system Python instead

## 4. Running the Analysis

Since the experiment data already existed, I ran:
```bash
python3 src/analyze_results.py
```

### Results Obtained

The analysis successfully reproduced the original findings:

**Response Length:**
- Human-style prompts: Mean = 95.5 tokens (SD = 86.1)
- AI-style prompts: Mean = 114.0 tokens (SD = 105.8)
- **Difference: ~19% longer responses to AI-style prompts**
- Statistical test: t = -2.0268, p = 0.052 (marginally significant)

**Sentiment:**
- Human-style prompts: Mean = 0.087
- AI-style prompts: Mean = 0.065
- Statistical test: t = 0.8549, p = 0.400 (not significant)

**Refusal Rate:**
- Human-style prompts: 0%
- AI-style prompts: 3.3%

### Plots Generated

The analysis created three visualizations in `results/plots/`:
- `length_comparison.png` - Box plot showing response length distribution
- `sentiment_comparison.png` - Box plot showing sentiment scores
- `refusal_comparison.png` - Bar plot showing refusal rates

## 5. Understanding the Code

I reviewed all source files to understand the methodology:

**`utils.py`**: Helper functions for calling LLM APIs with retry logic

**`generate_prompts.py`**: Takes human questions from the HC3 dataset and uses GPT-4 to create AI-style paraphrases, creating paired prompts with identical meaning but different styles

**`run_experiment.py`**: Sends both prompt versions to GPT-4o and collects responses for comparison

**`analyze_results.py`**: Performs statistical analysis (paired t-tests) and creates visualizations

## 6. Key Findings

The experiment demonstrates **style mirroring** behavior in LLMs:

1. **GPT-4o produces longer responses** (~19% more tokens) when prompted with AI-style text
2. The effect is marginally significant (p = 0.052)
3. No significant differences in sentiment or refusal rates
4. This suggests LLMs adapt their verbosity to match the input style

## 7. What I Learned

### Technical Skills
- Working with JSONL datasets
- Making API calls to LLMs
- Statistical hypothesis testing (paired t-tests)
- Data visualization with matplotlib/seaborn
- Python data processing with pandas

### Research Methodology
- Controlled experimental design (paired comparisons)
- Importance of controlling for semantic content while varying style
- Multiple dependent variables strengthen conclusions
- Reproducibility through random seeds and documented parameters

### Software Engineering
- Handling dependency issues
- Reading and understanding others' code
- Error handling and debugging
- File I/O and data serialization

## 8. Conclusions

I successfully reproduced the analysis phase of this experiment and confirmed the original findings. The code is well-structured and demonstrates good research practices including:
- Clear separation of concerns (data generation, experiment, analysis)
- Comprehensive error handling
- Documented parameters for reproducibility
- Multiple metrics for robust conclusions

The research provides interesting evidence that LLMs exhibit style mirroring, matching the formality and verbosity of their inputs. This has implications for prompt engineering and understanding LLM behavior.

## 9. Future Directions

Potential extensions of this work could include:
- Testing other LLM models (Claude, Gemini, etc.)
- Varying the degree of formality/verbosity
- Testing with different question domains
- Analyzing other response characteristics (structure, examples used, etc.)
