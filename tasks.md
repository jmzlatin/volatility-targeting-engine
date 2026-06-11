# tasks.md

Development tracker for the Volatility Targeting Position Sizing Engine. Update this file as work progresses.

## Phase 1: Data Cache and Ingestion

- [ ] Define the `data/` module structure and public interface.
- [ ] Implement yfinance price downloads for a configurable ticker list and date range.
- [ ] Build a local cache layer to store downloaded price series and avoid repeated network calls.
- [ ] Add cache invalidation based on date staleness.
- [ ] Clean raw data: handle missing values, align trading calendars, and drop incomplete rows.
- [ ] Compute daily returns from adjusted close prices.
- [ ] Validate that fetched series match requested tickers and dates.

## Phase 2: Risk Mathematics

- [ ] Implement trailing annualized volatility from a configurable lookback window.
- [ ] Apply the annualization factor (square root of trading days per year).
- [ ] Implement inverse-volatility asset weights from the fixed risk constant.
- [ ] Cap weights at a maximum leverage bound to prevent extreme position sizes.
- [ ] Handle edge cases: zero volatility, insufficient lookback data, and NaN inputs.
- [ ] Verify the risk layer imports and runs with no data or frontend dependencies.

## Phase 3: Streamlit Interface

- [ ] Build the main app entry point in `app/main.py`.
- [ ] Add input controls for tickers, lookback window, target volatility, and date range.
- [ ] Render the performance timeline comparing the targeted strategy against the raw asset.
- [ ] Render the drawdown comparison chart for both series.
- [ ] Display key metrics: realized volatility, max drawdown, and cumulative return.
- [ ] Show the current position weight derived from the latest volatility estimate.

## Phase 4: Unit Test Suite

- [ ] Set up pytest configuration and the `tests/` directory.
- [ ] Test data ingestion and cache hit and miss behavior with mocked yfinance calls.
- [ ] Test trailing annualized volatility against known fixtures.
- [ ] Test inverse-volatility weight output, including the leverage cap.
- [ ] Test edge cases: zero volatility, short series, and NaN handling.
- [ ] Add a regression test for the full data-to-weight pipeline.
- [ ] Confirm the suite runs clean with `pytest`.
