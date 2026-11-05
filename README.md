# Forecast Studio

Interactive 2D / 3D stock time series forecasting lab, built for the GenAI internship's Project 2: Thinking in HTML.

## Overview

Explore how different forecasting methods use historical stock prices, compare their errors on unseen observations, and inspect possible future price paths in an interactive 3D scene. The application uses synthetic prices for fictional stocks; it does not connect to a stock exchange or market API.

This is the first HTML page of the three-page Project 2 assignment, not the complete three-page submission.

## Files

- **stock-forecast-lab.html** - Complete application, including styling, data generation, models, charts, and interactions.
- **prompts.txt** - User prompts and revision notes for the internship submission.
- **README.md** - Project overview and usage instructions.

## Run the project

1. Download or copy stock-forecast-lab.html to your computer.
2. Double-click the file to open it in a current browser such as Microsoft Edge, Chrome, or Firefox.
3. Switch between **2D timeline** and **3D scenarios** using the buttons above the chart.

No installation, account, API key, internet connection, build step, or local server is required. If the file opens in a text editor, right-click it and choose **Open with** followed by your browser. Refresh the browser after replacing the file with an updated version.

## Features

- Light blue-gray interface with orange, green, and blue accents.
- Four fictional market patterns: steady growth (ALPHA), cyclical (ORBIT), volatile (NOVA), and regime change (SHIFT).
- Four forecasting methods evaluated on the same test period.
- Adjustable forecast horizon, training window, market volatility, and nominal scenario band.
- 2D chart showing training prices, forecast, held-out actuals, and scenario band.
- Interactive 3D scenario surface with rotation, tilt, zoom, and point inspection.
- Front, side, top, and perspective camera presets, plus optional auto-rotation.
- Controls to hide actual prices, scenario paths, or the 3D surface.
- MAE and RMSE comparison table and a button to inspect the lowest-MAE model on the current split.
- CSV export and reproducible reset.
- Responsive layout and keyboard camera controls.

## Suggested demonstration

1. Start with ALPHA and the linear drift model.
2. Inspect the 2D forecast and its widening scenario band.
3. Hide actual prices, then reveal them to compare the forecast against the test period.
4. Change the forecasting model and compare MAE and RMSE.
5. Change the horizon or training window and observe how the results change.
6. Choose SHIFT to explore how a trend reversal challenges historical assumptions.
7. Open the 3D view, drag the chart, and try the camera presets.
8. Select a scenario and forecast session to inspect its simulated price.
9. Export the forecast as a CSV file.

## Controls

| Control | Behavior |
| --- | --- |
| Market pattern | Selects a fictional price-generation pattern |
| Forecast model | Selects the method used to predict the test period |
| Forecast horizon | Holds out the last 5-40 trading sessions for evaluation |
| Training window | Uses the preceding 20-100 observations for training |
| Market volatility | Changes the scale of noise in the synthetic market |
| Scenario band | Chooses an 80%, 90%, or 95% nominal band |
| Generate new market | Changes the random seed while retaining settings |
| Reset experiment | Restores the original market and default settings |
| Export forecast CSV | Downloads predictions, bands, settings, and visible actuals |

### 2D interaction

Hover over the chart or move a pointer across it to inspect a session's price. The divider marks the training cutoff. Blue shows training prices, green shows the forecast, and orange shows held-out actual prices.

### 3D interaction

- **Drag** to rotate the scene through different viewing angles.
- **Scroll or pinch** to zoom.
- Use **Rotate 360 degrees**, **Tilt**, and **Zoom** sliders for precise camera control.
- Choose **Perspective**, **Front**, **Side**, or **Top** for preset angles.
- Use **Auto rotate** to start or pause continuous rotation.
- Use **Reset camera** to restore the default perspective.
- Click a nearby scenario point, or use **Inspect scenario** and **Forecast session**, to inspect its value.
- Toggle **Show scenario surface** to reveal or hide the mesh.
- Focus the chart and use **arrow keys** to rotate; use **+** or **-** to zoom.

The three dimensions represent forecast time, simulated price, and scenario index. The depth axis separates simulated paths; it is not an additional financial variable.

## Data and forecasting methods

Each market contains 180 synthetic daily closing prices denominated in USD. With horizon H and training window W, the final H sessions form the held-out test period. Models see only the W sessions immediately before that period. Predictions are produced for the entire horizon without using held-out prices.

| Method | Assumption |
| --- | --- |
| Last-price baseline | Every future price equals the final training price |
| Linear drift | The mean daily price change across the training window continues |
| Moving-average level | Every future price equals the average of the last 10 training prices |
| Holt's trend smoothing | A smoothed level and trend continue into the forecast period; alpha = 0.35, beta = 0.12 |

The models are implemented directly in JavaScript. This application demonstrates forecasting concepts; it does not train a neural network or use an LLM to predict prices.

## Evaluation

- **MAE:** Mean absolute difference between predicted and held-out prices. Lower is better.
- **RMSE:** Root mean squared error. Larger mistakes receive more weight.
- **Vs. last-price baseline:** Percentage MAE reduction relative to the baseline. Negative values mean the selected model performed worse.

The lowest-MAE model is selected retrospectively from the current test split. This is an explanation of that split, not evidence of future superiority.

## Scenario bands and limitations

The band is a teaching approximation:

Forecast at step h +/- z * standard deviation of training price changes * square root of h.

The nominal percentage assumes independent Gaussian changes. It is not calibrated coverage for every model, this synthetic generator, or real stock markets. The 17 scenario paths add cumulative Gaussian noise to the forecast; they are illustrative simulations, not separate trained models.

Other limitations:

- All stocks and prices are fictional; no live or historical market dataset is included.
- Evaluation uses one held-out split, not rolling cross-validation.
- Transaction costs, dividends, market news, liquidity, and trading execution are not modeled.
- Results are educational and should not be used as trading recommendations.

## Technology

- HTML5 for page structure and native form controls.
- CSS for the responsive interface.
- Vanilla JavaScript for models, state, interactions, and CSV export.
- Canvas 2D for the timeline and perspective-projected 3D scene, including depth-sorted surfaces and camera transformations.
- No external libraries or assets.

## Verification performed

After repairing a script-block duplication issue, the JavaScript compiled successfully and passed 16 startup, rendering, and interaction regression checks in a simulated DOM/canvas environment. Both chart modes were also visually checked in Microsoft Edge, and dragging was confirmed to change the 3D angle. This does not constitute exhaustive testing across every browser or mobile device.

## Internship submission

Keep this HTML file and the prompt log for the final Project 2 folder. The assignment also requires two additional HTML pages from different project options. Once all three pages are complete, package the final pages and ordered prompts in one ZIP under 10 MB, using the required YourName_Project2.zip naming format.
"# forecast_stocks_time_series" 
