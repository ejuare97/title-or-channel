# Title or Channel? Title features and views of Spanish-language YouTube videos

Code and derived data for the article *Title or Channel? Disentangling the Contribution of Title Features to the Views of Spanish-Language YouTube Videos* (anonymous submission).

## Contents

| Path | Description |
|---|---|
| `src/01_extraccion.ipynb` | Extracts long-form videos from 23 channels with the YouTube Data API v3 (Google Colab). |
| `src/02_analisis.ipynb` | Language filter, title features, sentiment, ablation C1–C4, leave-one-channel-out validation, mixed model, SHAP (Google Colab, GPU recommended). |
| `data/video_ids.csv` | `channel_id` and `video_id` of the 3,051 videos analysed (21 channels). |

## Data

- Extraction date: 2026-11-11 (06:46:11 UTC). Up to 150 long-form videos per channel (≥ 180 s, ≥ 7 days old, no live streams or premieres, public view count).
- Raw extraction: `youtube_videos_largos_20261111_064611.csv`, 3,351 videos from 23 channels.
  SHA-256: `FC152A7089DEE9F87BCACFBC678DEB4F542345B121E35D5C08DC8B2AC9AEA792`
- Analysed corpus: 3,051 videos from 21 channels. Two channels owned by a creator already in the corpus (`SEGUN EL GEORGE`, `Cultura VJ`) are excluded in cell 1 of `02_analisis.ipynb` (`EXCLUIR_CANALES`), so that each creator is a single group.
- Titles, descriptions, tags and view counts come from the YouTube API and are not redistributed here. Video IDs are provided so that the metadata can be requested again; view counts change over time, so a new extraction will not match the original exactly.

## How to reproduce

1. Create a YouTube Data API v3 key and store it as the Colab secret `YT_API_KEY`.
2. Run `src/01_extraccion.ipynb` (about 300–600 quota units). Download the generated `youtube_videos_largos_*.csv`.
3. Run `src/02_analisis.ipynb` in order, cells 0 to 4b, and then cells 5 to 13. Upload the CSV in cell 0.

Fixed seed: 42. All Random Forests use 200 trees. The target is `log10(views + 1)`.

## Requirements

Google Colab (Python 3). The notebooks install `vaderSentiment`, `dcor`, `emoji`, `shap` and `pysentimiento`; `scikit-learn`, `scipy`, `statsmodels` and `pandas` come preinstalled.
