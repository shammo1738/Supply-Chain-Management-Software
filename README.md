# Supply-Chain-Management-Software
Supply Chain demand forecasting app built from scratch. Generates dummy data and lets you tune noise/seasonality. Includes 8 methods (SMA, WMA, SES, regression, Holt, Holt-Winters, seasonal naive, decomposition) with charts, approximate 95% prediction intervals, and metrics (MAE, MAPE, RMSE, tracking signal). Auto-picks best via lowest MAPE.

Live app: https://shammo1738.github.io/Supply-Chain-Management-Software/

## How to use
The app looks at your past monthly sales and predicts the next few months. The same guide is in the app's **How to Use** tab.

### 1. Load your data (Data tab)
Pick one of three ways:
- **Just trying it out?** Under *Generate Sample Data*, choose a time range, seasonality, trend and noise level, then click **Generate Data**. 2 years or more works best.
- **Have a spreadsheet?** Save it as a CSV and drag it onto *Import CSV* (or click the box to browse).
- **Only a few numbers?** Type them into *Manual Entry*, use **+ Add Row** for more, then click **Load Data**.

Your CSV needs a date column and a quantity column. Product and revenue columns are optional:

```csv
Date,Product,Quantity,Revenue
2024-01-15,Widget A,120,2400
2024-02-15,Widget A,135,2700
2024-03-15,Widget A,128,2560
```

The app finds columns by their headers. The date header should contain `date`, `month`, `period` or `time`. The quantity header should contain `quantity`, `qty`, `units`, `sales` or `demand`. Check the *Data Preview* that appears, and click **Save Dataset** if you want to reload it later.

### 2. Choose forecasting methods (Forecast tab)
Tick the methods you want to try. If you're not sure, tick them all.
- **Simple / Weighted Moving Average:** averages the last few months. Good for steady demand.
- **Exponential Smoothing:** a smoother average that gives recent months more weight.
- **Linear Regression and Holt's:** follow a rising or falling trend.
- **Holt-Winters, Seasonal Naive and Seasonal Decomposition:** handle repeating yearly patterns, like holiday peaks.

You need at least 4 months of data. With the default 12-month season, Seasonal Naive needs 13 months, and Holt-Winters and Seasonal Decomposition need 24. Methods without enough data are skipped, and the app tells you why.

### 3. Set it up and run the forecast
- **Forecast Horizon:** how many months ahead to predict (1 to 24).
- **Product Filter:** forecast one product, or all products added together.
- **Method sliders (optional):** the defaults are sensible. A bigger window or a smaller alpha gives a smoother forecast that reacts more slowly to change.

Click **Run Forecast**. The chart shows your history and each method's prediction. The shaded band around the best method is an approximate 95% range.

### 4. Find the most accurate method (Compare tab)
The method with the lowest MAPE is marked as the **Best Method** (see [How accuracy is measured](#how-accuracy-is-measured)).
- **MAPE:** average error as a percentage. Lower is better.
- **MAE:** average error in units.
- **RMSE:** like MAE, but punishes big misses more.
- **Tracking Signal:** shows whether a method keeps guessing too high or too low. Close to 0 is good; beyond about ±4 means it's consistently off in one direction.

The best method is used for the report automatically. Click **Use for Report** to pick a different one.

### 5. Get your forecast (Report tab)
The report lists the predicted value for each future month with a low and high estimate. Use the range to plan safety stock, not just the single number. Then **Print / Save PDF**, **Export CSV** (opens in Excel) or **Copy to Clipboard**.

### Tips
- More history is better. Two or more years lets the app pick up seasonal patterns.
- If one product behaves very differently from the rest, forecast it on its own with the Product Filter.
- Re-run the forecast each month as new sales come in.

## How accuracy is measured
Every method is scored on honest one-step-ahead forecasts: each month is predicted using only the months before it. All methods are scored on the same months, so the "best method" comparison is fair.

## Data input
- Upload a CSV with a date column and a quantity column (product and revenue columns are optional), enter data manually, or generate sample data.
- Supported date formats include `2024-01-15`, `2024-01`, `01/15/2024`, `15/01/2024`, `Jan 2024` and `January 15, 2024`.
- Data is grouped by month. Months with no sales are counted as 0.
- Everything runs in your browser. Saved datasets stay in your browser's local storage.

## Third-party libraries
- [Chart.js](https://www.chartjs.org/) (MIT License)
- [PapaParse](https://www.papaparse.com/) (MIT License)

## License
MIT License. See [LICENSE](LICENSE).
