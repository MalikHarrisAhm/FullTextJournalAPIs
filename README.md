# Academic Paper Text Extraction Tool

This tool helps researchers automatically extract full text content from academic papers across multiple scholarly databases. It supports several major academic publishers and preprint servers, providing a streamlined way to collect paper content for research purposes.

## Features

- Multi-source text extraction from:
  - NCBI/PubMed Central
  - Springer
  - Elsevier
  - Wiley
  - bioRxiv
  - medRxiv
  - arXiv
- Progress tracking with detailed statistics
- Automatic rate limiting to respect API constraints
- Periodic saving of results to prevent data loss
- Detailed success/failure statistics per source
- Graceful interrupt handling with statistics output

## Prerequisites

- Python 3.7 or higher
- API keys for the following services (as needed):
  - Springer
  - Elsevier
  - Wiley

## Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/paper-text-extraction.git
cd paper-text-extraction
```

2. Install required dependencies:
```bash
pip install pandas requests tqdm python-dotenv
```

3. Create necessary directories:
```bash
mkdir input output
```

## Configuration

1. Create a `.env` file in the project root with your API keys:
```plaintext
SPRINGER_API_KEY=your_springer_key
ELSEVIER_API_KEY=your_elsevier_key
WILEY_API_KEY=your_wiley_key
NCBI_TOOL_NAME=your_tool_name
NCBI_EMAIL=your_email@example.com
```

2. Prepare your input CSV file:
   - Place it in the `input` directory
   - Ensure it has a `DOI` column containing paper DOIs
   - Name it `dimensions_dataset.csv` or update the filename in the script

## Usage

1. Run the script:
```bash
python text_extraction.py
```

2. Monitor the progress:
   - The script shows a progress bar with current statistics
   - Statistics are updated in real-time
   - Results are saved every 10 papers processed

3. Find the results:
   - Output is saved to `output/text_extraction.csv`
   - Includes original data plus:
     - `Full Text`: Extracted text content
     - `TXT or PDF`: Source of the extracted content

## Interrupt Handling

- Press `Ctrl+C` to safely stop the script
- Final statistics will be displayed, including:
  - Time elapsed
  - Papers processed
  - Success/failure counts
  - Per-source statistics

## Example Output Statistics

```
Processing Statistics:
Processed 100 out of 500 papers (20.0%)
Success: 75 papers
Failed: 25 papers
Success Rate: 75.00%

Source Statistics:
Source          Success    Attempts   Success Rate    % of Total Success
--------------------------------------------------------------------------------
NCBI            30         40         75.0%          40.0%
Springer        20         25         80.0%          26.7%
Elsevier        15         20         75.0%          20.0%
Wiley           10         15         66.7%          13.3%
```

## Rate Limiting

The script includes a 0.1-second delay between requests to avoid overwhelming APIs. Adjust this value in the code if needed:

```python
time.sleep(0.1)  # Adjust as needed
```

## Troubleshooting

1. Missing API Keys:
   - Ensure your `.env` file exists and contains all required keys
   - Check for any spaces or quotes in the `.env` file
   - Verify API key validity with the respective services

2. Connection Issues:
   - Check your internet connection
   - Verify API service status
   - Ensure you haven't exceeded API rate limits

3. Input File Issues:
   - Verify CSV file exists in the input directory
   - Ensure CSV has a 'DOI' column
   - Check for proper CSV formatting

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Thanks to all the academic publishers providing API access
- Built with Python and essential libraries: pandas, requests, tqdm
- Inspired by the need for automated academic text extraction

## Disclaimer

Please ensure you have the necessary rights and permissions to access and store the paper content you're extracting. Respect the terms of service and usage limits of each API provider.
