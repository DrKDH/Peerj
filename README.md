ECIA: Emotionally-Guided Contextual Intelligence Agent
Description
ECIA is a reinforcement learning agent that incorporates emotional processing, episodic memory, and adaptive dopamine-based learning for multi-environment decision making. The system evaluates agent performance across multiple environments and provides comprehensive statistical analysis with cross-dataset validation.
Dataset Information
Primary Data Files (.npy format)
•	emotion_data_EnvA.npy: Emotional dynamics data for Environment A (50 runs × 200 trials × 8 emotions)
•	emotion_data_EnvB.npy: Emotional dynamics data for Environment B (50 runs × 200 trials × 8 emotions)
•	emotion_data_EnvC.npy: Emotional dynamics data for Environment C (50 runs × 200 trials × 8 emotions)
Experimental Results (.pkl format)
•	complete_results_full.pkl: Complete experimental results across all environments (12 master seeds × 300 runs)
•	complete_cross_dataset_results_unified.pkl: Cross-dataset comparison results
•	bonferroni_correction_results.pkl: Multiple comparison correction results

Data Format
•	.npy files: NumPy arrays with shape [n_runs, n_trials, n_emotions], float64, range [0.0, 1.0]
•	.pkl files: Python dictionaries containing statistical results, performance metrics, and experimental metadata

Code Information
Main Scripts
•	ECIA_code.py: Primary implementation including ECIA agent, environment classes, and meta-analysis framework
•	pkl_review.py: Post-processing script for analyzing stored experimental results

Key Components
•	Agent Classes: ECIA (full), EpsilonGreedyAgent, UCBAgent, ThompsonSamplingAgent
•	Environment Classes: EnvironmentA, EnvironmentB, EnvironmentC, RandomShiftEnvironment
•	Ablation Variants: ECIA_NoEmotion, ECIA_NoMemory, ECIA_NoDopamine, etc.

Usage Instructions

Quick Start (Using Pre-computed Results)
Prerequisites 
Ensure the following data files are available:
 - complete_results_full.pkl -complete_cross_dataset_results_unified.pkl  
- emotion_data_EnvA.npy, emotion_data_EnvB.npy, emotion_data_EnvC.npy (optional for emotion analysis)

# Analyze pre-computed experimental results
python pkl_review.py

Running New Experiments

# Generate new experimental data (long runtime)
python ECIA_code.py

Expected Output Files
•	envA-C_wide_format.csv: Environment A-C comprehensive statistics
•	significant_results_bonferroni.csv: Statistical significance results after multiple comparison correction
•	emotion_trajectories_Env(A,B,C).png: Emotion trajectory visualizations
•	emotion_comparisons_all_environments.png: Combined emotion analysis

Requirements
numpy>=1.21.0
pandas>=1.3.0
matplotlib>=3.4.0
scipy>=1.7.0
seaborn>=0.11.0
tqdm>=4.62.0

Methodology
Experimental Design
•	Environment A: Deterministic reward structure with change points at trials 50, 100, 150
•	Environment B: Alternating optimal actions every 40 trials with low noise
•	Environment C: Stochastic environment with random change points and disturbances
Evaluation Method
The study employs cross-validation with ablation studies as the primary evaluation approach:
1	Meta-analysis Design: 12 Fibonacci master seeds × 300 runs = 3,600 experiments per agent per environment
2	Cross-dataset Validation: Sequential training on Environments A→B→C, then testing on RandomShift environment
3	Statistical Validation: Multiple comparison correction using Bonferroni method with appropriate test selection:
◦	Student's t-test (normal distributions, equal variances)
◦	Welch's t-test (normal distributions, unequal variances)
◦	Mann-Whitney U test (non-normal distributions)
4	Ablation Studies: Systematic removal of ECIA components (emotion, memory, dopamine systems)
Assessment Metrics
•	Overall Performance: Mean reward across all trials
•	Recovery Rate: Proportion of successful performance recovery after environmental changes
•	Recovery Time: Number of trials required to return to baseline performance
•	Emotional Dynamics: 8-dimensional emotion trajectory analysis

Data Preprocessing Steps 
Not applicable - All environments generate synthetic data in ready-to-use format. No external data preprocessing is required.

Data Processing
•	Seed Management: Fibonacci sequence master seeds for reproducible meta-analysis
•	Quality Control: Success rate monitoring and statistical validation
•	Preprocessing: Automatic context normalization, emotion state regulation, and reward clipping
Computing Infrastructure
•	Operating system : python 3.8+ compatible (Windows, macOS, Linux)
•	Runtime : Approximately 5-6 hours for complete experiment

Contact Information
•	Primary Author: Daihun Kang
•	Email: gpk1234567@naver.com
•	Institution: Ewha Women's University, Seoul, Korea
