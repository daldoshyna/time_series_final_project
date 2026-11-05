# MATH840 Final project

The notebook forecasts the next 48 hours of hourly electricity generation (2026-10-27 01:00 to 2026-10-29 00:00) with a 95% prediction interval.

**Final model:** `HarmARMA_K4+SNaive`, an equal-weight blend of
1. a harmonic regression with ARMA errors (2 daily Fourier harmonics, ARMA(2,0,1) errors, fitted on `log(y + 20)` using the last 28 days), and
2. the seasonal-naive forecast (repeat yesterday).

## Files

| File | Purpose |
|---|---|
| `notebook.ipynb` | The full analysis: EDA, backtest of all candidate models, and the submission |
| `train.csv` | Input: hourly history with weather (from Moodle) |
| `weather_forecast.csv` | Input: weather forecast for the 48 forecast hours (from Moodle) |

## Requirements

- Python 3 with Jupyter, or Google Colab.
- Packages: `numpy`, `pandas`, `matplotlib`, `statsmodels`, `statsforecast`.
- The first code cell installs everything with the pinned versions from the course template:

```
!pip install -q statsforecast==2.1.1 neuralforecast==3.3.0 chronos-forecasting==2.3.2 "timesfm[torch]==3.0.2" tirex-ts==1.4.2
```

  The model code itself only uses the packages listed above. The other packages in that line come from the course template and are not used. The `!pip` line works in Jupyter and Colab. If you run the notebook as a plain Python script, install the packages manually.

## How to run

1. **Put the data in place.** The cell that loads the data reads the files from `../../../../Downloads/train.csv` and `../../../../Downloads/weather_forecast.csv`. Either put the two files there, or change those two paths in that cell to `train.csv` and `weather_forecast.csv` and put the files next to the notebook. On Colab, upload the files and use the shorter paths.
2. **Check `SURNAME`** in the first code cell (`"Aldoshyna"`). It determines the output file name.
3. **Run all cells from top to bottom** (Runtime → Run all in Colab, or Kernel → Restart & Run All in Jupyter). The cells depend on each other, so they must run in order.
4. **Wait for the backtest cell.** The cell in section 3 (the one that prints `вікон: 104, ...`) fits every candidate model on 104 rolling windows. It takes about 5 minutes. The slowest models are `HarmARMA_K6` and `HarmARMA_Weekly`, about one minute each.
5. **Read the output.** The submission cell in section 4 prints the first rows of the forecast, the next cell plots the last 7 days of history with the forecast and the interval, and the last cell checks the format and saves the file.

When it works, the last cell prints `format OK` and `saved ALDOSHYNA_project.csv`. On Colab the file is also downloaded automatically.

## Reproducibility

The code has no random components. The same data gives the same forecast.

## AI Usage

I used AI to:
- write some of the code
- search for alternative solutions (for example, to search for alternative models to try using, beyond simple ETS/ARIMA)
- rephrase some parts of my report and README to make it more concise
