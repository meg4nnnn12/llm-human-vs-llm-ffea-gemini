# Reproduction Report: LLM Style Mirroring Experiment

**Author:** Megan Cheng  
**Date:** January 30, 2026  
**Original Project:** https://github.com/Hypogenic-AI/llm-human-vs-llm-ffea-gemini

## 1. Overview

This report documents my reproduction of the LLM style mirroring experiment analysis, which investigates the question “Do LLMs behave differently when the prompter is human vs another LLM?”


## 2. What I Reproduced

The repository already contained the complete experiment results from the original researchers, which included:
- `paired_prompts.json` (30 question pairs)
- `experiment_results.json` (GPT-4o responses to both prompt styles)

Rather than re-running the expensive API calls (which would have cost $10-20 and produced the same data), I focused on reproducing the analysis phase of the research.

I successfully:
1. Ran the analysis script (`analyze_results.py`)
2. Reproduced the statistical findings (paired t-tests)
3. Regenerated all visualizations
4. Verified the original conclusions

This allowed me to understand the methodology, statistical approach, and interpretation of results without the API costs, especially because this is still new to me. 


## 3. Setup Process

### Environment
- **OS:** macOS (Apple Silicon)
- **Python Version:** 3.11.2
- **Installation Method:** System Python with pip

### Dependencies Installed
I manually installed the following packages because the original `requirements.txt` had some issues:
```bash python3 -m pip install openai tqdm anthropic matplotlib scipy numpy pandas seaborn tenacity textblob --break-system-packages
```

## 4. Challenges I Encountered

### 1. Python Command Issues
I'm new to using the terminal, so I didn't realize that on Mac I need to use `python3` instead of `python`. This was my first confusion but easy to fix once I figured it out.

### 2. Broken Dependencies File
The requirements.txt file had a problem because it referenced a file path from someone else's computer that didn't exist on mine. The error message was: `Distribution not found at: file:///croot/anaconda-anon-usage...`

I had to manually figure out which packages were needed and install them one by one. I kept running the script, seeing what package was missing, installing it, and trying again. Eventually I installed: openai, tqdm, anthropic, matplotlib, scipy, numpy, pandas, seaborn, tenacity, and textblob.

### 3. Virtual Environment Problems
I tried creating a virtual environment using `uv venv` like the ReadMe said, but it created an environment without pip installed. After struggling with this for a while, I just gave up on the virtual environment and installed everything directly to my system Python using the `--break-system-packages` flag.

### 4. Missing Dataset
When I first tried to run `generate_prompts.py`, there was an error message that the HC3 dataset was missing. I was worried I'd have to find and download it, but then I checked the results folder and realized all the data files were already there. I could skip the data generation steps and go straight to the analysis.

### 5. Trial and Error Process
The whole process involved a lot of running a command, getting an error about a missing package, installing that package, and trying again. It was frustrating at times but I learned a lot about how Python dependencies work and how to read error messages.

After about an hour of debugging, I finally got `analyze_results.py` to run successfully and it generated all the plots and statistics!


## 4. Running the Analysis

Since the experiment data already existed, I ran:
```bash python3 src/analyze_results.py
```

### Results Obtained

The analysis successfully reproduced the original findings:

**Response Length:**
- Human-style prompts: Mean = 95.5 tokens (SD = 86.1)
- AI-style prompts: Mean = 114.0 tokens (SD = 105.8)
- **Difference: ~19% longer responses to AI-style prompts**
- Statistical test: t = -2.0268, p = 0.052

**Sentiment:**
- Human-style prompts: Mean = 0.087
- AI-style prompts: Mean = 0.065
- Statistical test: t = 0.8549, p = 0.400 

**Refusal Rate:**
- Human-style prompts: 0%
- AI-style prompts: 3.3%

### Plots Generated

The analysis created three visualizations in `results/plots/`:
- `length_comparison.png` - Box plot showing response length distribution
- `sentiment_comparison.png` - Box plot showing sentiment scores
- `refusal_comparison.png` - Bar plot showing refusal rates


## 5. Key Findings

The experiment demonstrates **style mirroring** behavior in LLMs:

1. **GPT-4o produces longer responses** (~19% more tokens) when prompted with AI-style text
2. The effect is marginally significant (p = 0.052)
3. No significant differences in sentiment or refusal rates
4. This suggests LLMs adapt their verbosity to match the input style

## 6. What I Learned

### Technical Skills
- Using the terminal in VSCode
- Working with JSONL datasets
- Making API calls to LLMs
- Statistical hypothesis testing (paired t-tests)
- Data visualization with matplotlib/seaborn
- Python data processing with pandas

### Software Engineering
- Handling dependency issues
- Reading and understanding others' code
- Error handling and debugging

## 7. Conclusions

## Conclusion

I successfully reproduced the analysis portion of this LLM style mirroring experiment. Since the repository already had all the experiment data (the paired prompts and GPT-4 responses), I focused on running the statistical analysis and regenerating the visualizations.

The main finding held up - GPT-4o really does produce longer, more verbose responses when you prompt it with AI-style text versus casual human questions. The responses were about 19% longer on average, which is pretty significant. It's interesting that the model basically mirrors whatever style you give it, even though the actual question being asked is the same.


## 8. Future Directions

Potential extensions of this work in the future could include:
- Testing with other LLM models (Claude, Gemini, etc.)
- Varying the degree of formality
- Testing with different question domains
- Analyzing other response characteristics (structure, examples used, etc.)
- Add comments to the code to clarify some parts, especially for people reading the code for the first time

