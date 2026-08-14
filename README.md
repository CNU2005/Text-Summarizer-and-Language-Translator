# Text Summarizer & Language Translator

A Python desktop application that summarizes long text into key points and translates it into multiple Indian and global languages — all from a simple Tkinter GUI.

## Features

- **Extractive Text Summarization** — Uses TF-IDF (via `scikit-learn`) to score sentences by importance and pull out the most representative ones, while preserving thematic coverage across paragraphs.
- **Automatic Language Detection** — Detects the language of any input text before processing.
- **Multi-language Translation** — Translates text to and from 12+ languages including Hindi, Telugu, Tamil, Kannada, Malayalam, Urdu, Bengali, Chinese, Japanese, Russian, French, and English.
- **Summarize in Any Language** — Non-English input is translated to English for accurate summarization, then translated back into your chosen output language.
- **Simple Desktop GUI** — Built with Tkinter: paste text on one side, get results on the other.

## Tech Stack

| Component | Library |
|---|---|
| GUI | `Tkinter` |
| Summarization | `NLTK`, `scikit-learn` (TF-IDF) |
| Translation | `Googletrans` |
| Numerical ops | `NumPy` |

## Project Structure

```
Text-Summarizer-and-Language-Translator/
├── Main.py          # Entry point — launches the Tkinter app
├── gui.py           # TextProcessorApp — UI layout and event handlers
├── summarizer.py    # TF-IDF extractive summarization logic
├── translator.py     # Language detection & translation via googletrans
├── requirements.txt  # Python dependencies
└── README.md
```

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/CNU2005/Text-Summarizer-and-Language-Translator.git
   cd Text-Summarizer-and-Language-Translator
   ```

2. **Create a virtual environment** (recommended)
   ```bash
   python -m venv venv
   source venv/bin/activate      # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Download the required NLTK data** (only needed once)
   ```bash
   python -m nltk.downloader punkt
   ```

## Usage

Run the application:

```bash
python Main.py
```

1. Paste or type your text into the **left panel**.
2. Choose your **Summarize in** language and click **Summarize** for a condensed version, or choose a **Translate to** language and click **Translate** for a full translation.
3. View the result in the **right panel**.
4. Click **Clear** to reset both panels.

## How Summarization Works

1. The input text is split into sentences using NLTK's sentence tokenizer.
2. Each sentence is vectorized with TF-IDF and scored by its cumulative term weight.
3. The text is also split into paragraphs ("thematic sections") so that summary sentences are drawn proportionally from each section — this keeps the summary from over-representing a single dense paragraph.
4. The highest-scoring sentences from each section are selected, re-ordered to match their original sequence, and joined into the final summary.
5. Summary length defaults to ~25% of the original word count (minimum 5 words).

## Requirements

```
nltk
numpy
scikit-learn
googletrans==4.0.0-rc1
```

## Known Issues & Notes

- **`googletrans` stability**: This project uses the unofficial `googletrans` library, which relies on reverse-engineered Google Translate endpoints. It can break unexpectedly if Google changes its API. If translation calls start failing, try pinning `googletrans==4.0.0-rc1` or switching to the official `google-cloud-translate` API (requires an API key).
- **Language support**: Summarization is optimized for English; non-English text is auto-translated to English first, which means summary quality depends on translation accuracy.
- **Large texts**: Very long inputs may take longer to process due to translation round-trips.

## Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request for bug fixes, new language support, or alternative summarization strategies (e.g., abstractive summarization with transformer models).

## License

This project is open source. Add a license file (e.g., MIT) if you plan to distribute it.
