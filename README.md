 Who Is Speaking? How Large Language Models Reshape Trauma Memory

Code and results for the MA thesis *"Who Is Speaking? How Large Language Models Reshape Trauma Memory"* (University of Amsterdam, 2026), supervised by Tobias Blanke.

## Overview

This thesis examines how large language models structurally distort personal COVID-19 testimony when processed alongside official institutional discourse. Using the JOTPY (*A Journal of the Plague Year*) oral history archive as a corpus of personal testimony and World Health Organization press briefings as a corpus of official discourse, the analysis proceeds across three computational stages:

1. **Word embeddings** — Word2Vec models trained separately on each corpus, aligned via orthogonal Procrustes, and compared for semantic drift across a set of focus words.
2. **Hidden states** — Layer-wise hidden state extraction from BERT-base-uncased and Llama-3.2-1B, measuring how representations of personal and official sentences diverge or converge across transformer layers.
3. **Text generation** — Claude Haiku generation under four context conditions (no context, personal-only, official-only, mixed), measuring how source material conditions model output.

## Data

This repository does **not** include the raw text of the JOTPY personal testimonies.

JOTPY testimonies are personal accounts of trauma shared by contributors to a public archive. Redistributing the raw transcripts outside that archive's intended context raises the same ethical concerns this thesis examines, so they are not reproduced here.

To reproduce the personal-corpus side of the analysis, obtain the testimonies directly from the archive: https://covid-19archive.org

The official corpus (`official_covid.txt`) consists of publicly released WHO COVID-19 press briefing transcripts (https://www.who.int) and is included in this repository.

Both corpora are expected as plain-text files (`personal_covid.txt`, `official_covid.txt`) with entries separated by a line of 60 dashes (`-` × 60). Place `personal_covid.txt` in the repository root (after obtaining it from JOTPY) before running the analysis scripts.

## Repository contents

| File | Description |
|---|---|
| `preprocessing` | Scraping and cleaning scripts for both corpora |
| `Word Embedding Analysis` | Word2Vec training, Procrustes alignment, t-SNE visualization, cosine distance analysis by word and by category |
| `Hidden States Analysis` | BERT and Llama hidden state extraction, layer-wise centroid distances, layer-to-layer movement analysis |
| `Generative Analysis` | Four-condition generation experiment and centroid-distance evaluation of generated text |
| `official_covid.txt` | WHO press briefing transcripts (public source material) |

## Results

The `results/` folder contains aggregated outputs only — figures, a nearest-neighbour table, and model-generated text. No verbatim personal testimony is included in any results file.

| File | Contents |
|---|---|
| `results/drift_distances.png` | Word-level cosine distance, personal vs. official (Procrustes-aligned) |
| `results/tsne_keywords.png` | t-SNE projection of focus words across both corpora |
| `results/neighbours_table.html` | Nearest-neighbour comparison table for focus words |
| `results/hidden_states_bert_full.png` | Layer-wise distance plot, BERT |
| `results/hidden_states_llama_full.png` | Layer-wise distance plot, Llama |
| `results/movement_analysis.png` | Layer-to-layer vector movement, personal vs. official (Llama) |
| `results/movement_comparison.png` | Movement magnitude and ratio comparison (Llama) |
| `results/movement_direction_v2.png` | Direction of movement relative to centroids (Llama) |
| `results/centroid_distances.png` | Generation experiment: distance to corpus centroids across four conditions |
| `results/four_conditions.json` | Model-generated responses across four conditions (question + response only; no source context included) |

## Environment

```
gensim
scikit-learn
matplotlib
scipy
numpy
transformers
torch
anthropic
huggingface_hub
```

API keys (Hugging Face, Anthropic) are read from environment variables and are never hardcoded:

```bash
export ANTHROPIC_API_KEY="your-key-here"
```

## Citation

If referencing this work, please cite the thesis directly. Contact details available via the University of Amsterdam.
