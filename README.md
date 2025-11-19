# Stock Price Predictor

This project is a machine learning project for predicting stock and ETF prices using historical data and deep learning models (LSTM). It includes data collection, preprocessing, model training, and prediction utilities.

## Features
- Download and preprocess historical NASDAQ stock and ETF data
- LSTM-based deep learning model for time series prediction
- Jupyter notebooks for data exploration, model training, and evaluation
- Modular structure for easy extension and experimentation

## Project Structure

```
├── pyproject.toml                # Project dependencies and metadata
├── data/                         # Data and data scripts
│   ├── data_clean.csv            # Cleaned dataset
│   ├── download-nasdaq-historical-data.ipynb  # Data download notebook
│   ├── symbols_valid_meta*.csv   # Symbol metadata (auto-generated)
│   ├── etfs/                     # ETF CSVs (auto-generated)
│   ├── stocks/                   # Stock CSVs (auto-generated)
│   └── invalid/                  # Invalid data (auto-generated)
├── predictor/                    # Model and prediction notebooks
│   ├── lstm-predictor.ipynb      # LSTM model training
│   ├── checker.ipynb             # Model evaluation
│   ├── model_config.json         # Model configuration (auto-generated)
│   └── stocks-lstm.weights.h5    # Trained model weights (auto-generated)
├── preprocessor/                 # Data preprocessing scripts
│   └── segment-symbols.ipynb     # Symbol segmentation
└── README.md                     # Project documentation
```

## Setup

1. **Python Version:** Requires Python 3.13+
2. **Install [uv](https://github.com/astral-sh/uv) (if not already installed):**
   ```sh
   curl -Ls https://astral.sh/uv/install.sh | sh
   # or see https://github.com/astral-sh/uv for other install methods
   ```
3. **Create a virtual environment and install dependencies:**
   ```sh
   uv venv  # make a virtual env
   uv run   # install dependencies
   ```
4. **Jupyter Notebooks:**
   Launch Jupyter Lab or Notebook to explore and run the provided notebooks.

## Usage

1. **Download Data:**
   - Use `data/download-nasdaq-historical-data.ipynb` to fetch and clean historical data.
   - Remember to change `download_etfs = 'N'` to `'Y' or 'N'` based on what data you want to download
   - You may also reduce the amount of data downloaded via `period = 'max'`
2. **Preprocess Data:**
   - Use `preprocessor/segment-symbols.ipynb` for symbol segmentation and preprocessing.
   - Separates ~50% of the csv files for training and testing
3. **Train Model:**
   - Run `predictor/lstm-predictor.ipynb` to train the LSTM model on your data.
   - Use 30 stocks in the following segments:
      - 5 of the stocks with the _least_ variance
      - 5 of the stocks with the _most_ variance
      - 5 of the stocks with variance roughly at the 25th percentile
      - 5 of the stocks with variance roughly at the 50th percentile
      - 5 of the stocks with variance roughly at the 75th percentile
      - 5 of any other random stocks
4. **Evaluate Model:**
   - Use `predictor/checker.ipynb` to evaluate predictions and visualize results.

## Dependencies

- keras
- tensorflow
- numpy
- pandas
- matplotlib
- scikit-learn
- yfinance
- jupyter, ipykernel

All dependencies are listed in `pyproject.toml`.

## License

This project is licensed under the MIT License.
