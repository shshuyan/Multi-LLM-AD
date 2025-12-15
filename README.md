# Multi-LLM-AD: Multi-LLM Evaluation for Alzheimer's Disease Clinical Trial Eligibility Criteria Extraction

## Overview

This repository contains research on extracting structured eligibility criteria from Alzheimer's Disease (AD) clinical trials using multiple Large Language Models (LLMs). The project evaluates and compares five state-of-the-art LLMs (GPT-4o, DeepSeek-R1, Gemini-2.5, KIMI-K2, Qwen3-max) for structured information extraction following the OpenAD schema.

## Project Structure

The project is organized into sequential studies, each addressing a specific research question:

- **`01_study1_direct_json_extraction.ipynb`**: Direct extraction of eligibility criteria as raw text from ClinicalTrials.gov JSON data
- **`02_study2_upstream_extraction.ipynb`**: Benchmark comparing different methods (API, LLM, embedding-based) for generating atomic {criterion_type, source_sentence} units
- **`03_gold_dataset_construction.ipynb`**: Construction of manually annotated gold standard dataset using the OpenAD schema
- **`04_ablation1_model_prompt.ipynb`**: Ablation study comparing different LLM + prompt combinations for extractor and verifier roles
- **`05_ablation2_stack_depth.ipynb`**: Ablation study on verification stack depth (2, 3, and 5 rounds) using Kimi-K2 verifier
- **`06_inspect_final.ipynb`**: Final inspection and evaluation of model performance across all 5 LLMs

## Data

- **`Raw_data/`**: Contains JSON files for 20 AD clinical trials downloaded from ClinicalTrials.gov API
  - Trial IDs: NCT01767311, NCT02008357, NCT02477800, NCT02484547, NCT03443973, NCT03444870, NCT03887455, NCT04437511, NCT04592341, NCT04619420, NCT04676360, NCT04770220, NCT04777396, NCT04828122, NCT05026866, NCT05108922, NCT05194540, NCT05269394, NCT05325008, NCT05531656

- **`final_gold.csv`**: Manually annotated gold standard dataset with 14-field OpenAD schema

## OpenAD Schema

The project uses a 14-field structured schema for eligibility criteria:

1. `trial_id`: Clinical trial identifier
2. `criterion_type`: Inclusion or exclusion criterion
3. `ad_domain`: Domain category (cognitive, biomarker, imaging, labs, comorbidity, functional, demographic, safety, treatment-history, AD-diagnostics)
4. `clinical_concept`: Specific clinical concept referenced
5. `operator`: Comparison operator (≥, ≤, >, <, =, between, present, absent, history-of, confirmed, etc.)
6. `value_lower`: Lower bound value (numeric string)
7. `value_upper`: Upper bound value (numeric string)
8. `units`: Measurement units
9. `diagnostic_framework`: Diagnostic framework used (e.g., NIA-AA)
10. `severity_stage`: Disease severity stage
11. `source_sentence`: Original sentence from trial eligibility criteria
12. `temporal_scope`: Temporal qualification (e.g., "at screening")
13. `evidence_type`: Type of evidence (clinical_exam, questionnaire, cognitive_test, etc.)
14. `certainty`: Certainty level (must, should, may, etc.)

## Models Evaluated

- **GPT-4o** (OpenAI)
- **DeepSeek-R1** (DeepSeek)
- **Gemini-2.5** (Google)
- **KIMI-K2** (Moonshot AI)
- **Qwen3-max** (Alibaba)

## Key Findings

The research systematically evaluates:
1. **Direct extraction methods**: Comparing raw text extraction approaches
2. **Upstream segmentation**: Identifying the best method for generating atomic criterion units
3. **Extractor-Verifier architecture**: Two-stage pipeline with separate extractor and verifier models
4. **Model combinations**: Testing different LLM pairings for extractor and verifier roles
5. **Verification depth**: Impact of multi-round verification stacks on extraction quality

## Setup

### Requirements

The notebooks require the following Python packages:
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `sentence-transformers` (for Study 2)
- API clients for the respective LLM providers

### API Keys

The notebooks require API keys for the LLM providers:
- `OPENAI_API_KEY`: For GPT-4o
- `GEMINI_API_KEY`: For Gemini-2.5
- `DEEPSEEK_API_KEY`: For DeepSeek-R1
- `QWEN_API_KEY`: For Qwen3-max
- `KIMI_API_KEY`: For KIMI-K2

Set these as environment variables or configure them in the notebook cells.

### Data Paths

**Note**: The notebooks currently use hardcoded paths pointing to `/Users/guoshuyan/Desktop/OpenAD`. You may need to update the `BASE_DIR` variable in each notebook to match your local setup.

## Usage

1. Start with `01_study1_direct_json_extraction.ipynb` to understand the direct extraction baseline
2. Proceed to `02_study2_upstream_extraction.ipynb` for upstream segmentation evaluation
3. Review `03_gold_dataset_construction.ipynb` to understand the gold standard annotation process
4. Run `04_ablation1_model_prompt.ipynb` to reproduce model×prompt ablation results
5. Execute `05_ablation2_stack_depth.ipynb` for stack depth analysis
6. Check `06_inspect_final.ipynb` for final model comparisons

## Citation

If you use this work, please cite:

```bibtex
@software{multi-llm-ad,
  title = {Multi-LLM-AD: Multi-LLM Evaluation for Alzheimer's Disease Clinical Trial Eligibility Criteria Extraction},
  author = {Shuyan, Guo},
  year = {2024},
  url = {https://github.com/shshuyan/Multi-LLM-AD}
}
```

## License

[Specify your license here]

## Contact

For questions or issues, please open an issue on GitHub or contact the maintainers.

