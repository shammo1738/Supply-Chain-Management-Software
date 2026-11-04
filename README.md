# Supply-Chain-Management-Software
Supply Chain demand forecasting app built from scratch. Generates dummy data and lets you tune noise/seasonality. Includes 8 methods (SMA, WMA, SES, regression, Holt, Holt-Winters, seasonal naive, decomposition) with charts, approximate 95% prediction intervals, and metrics (MAE, MAPE, RMSE, tracking signal). Auto-picks best via lowest MAPE.

Live app: https://shammo1738.github.io/Supply-Chain-Management-Software/

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
