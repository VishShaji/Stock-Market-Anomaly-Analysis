# Stock Market Anomaly Detection

## Executive Summary

This project focuses on detecting anomalies in stock market data using Z-scores of closing prices and trading volumes. By leveraging the Alpha Vantage API for data retrieval, we aim to identify unusual trading patterns that may indicate potential risks or opportunities for investors.

## Business Problem

In the volatile stock market, anomalies can signal significant events such as market manipulation, sudden price changes, or emerging trends. Identifying these anomalies in real-time can help investors make informed decisions, manage risks, and capitalize on opportunities. Traditional analysis methods may not effectively capture these anomalies, necessitating a more straightforward statistical approach. The Stocks used are Apple, Microsoft, Netflix, Google, and Tesla.

## Methodology

The project employs the following steps:

1. ### **Data Retrieval**:
   - Use the Alpha Vantage API to obtain stock market data, including closing prices and trading volumes.
  
   ![10 Rows of Data]((https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/data.head.png))
   ![Alt text](URL_or_Path_to_Image)
   - By plotting the adjusted close prices over time and trading volume over time, we can identify the general trend.
   
   ![Adjusted Close Prices](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/close.png)
   ![Trading Volume](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/volume.png)

3. ### **Data Preprocessing**:
   - Calculate Z-scores for the closing prices and trading volumes to identify anomalies.

   ![Z_score](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/z_score.png)

4. ### **Anomaly Detection**:
   - Identify anomalies based on the calculated Z-scores for both closing prices and volumes.

   ![Apple](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/AAPL.png)
   ![Netflix](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/NFLX.png)
   ![Microsoft](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/MSFT.png)
   ![Google](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/GOOG.png)
   ![Tesla](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/TSLA.png)

6. ### **Risk Assessment**

Compute risk scores using Python code that aggregates the Z-scores for anomalies:

- **Adjusted Close Risk**: This is calculated by grouping the identified anomalies in adjusted closing prices by ticker. For each ticker, the absolute mean of the Z-scores is computed, giving an indication of the average risk associated with price anomalies.

  ```python
  adj_close_risk = anomalies_adj_close.groupby('Ticker')['Z-score'].apply(lambda x: abs(x).mean())
  ```
  
- **Volume Risk**: Similarly, this is calculated by grouping the identified anomalies in trading volumes by ticker and computing the absolute mean of the Z-scores.

   ```python
   volume_risk = anomalies_volume.groupby('Ticker')['Z-score'].apply(lambda x: abs(x).mean())
   ```
   
- **Total Risk**: The total risk is then calculated by summing the adjusted close risk and volume risk for each ticker.
    ```python
      total_risk = adj_close_risk + volume_risk
    ```
    
- **Risk Rating**: Finally, a risk rating is computed to normalize the total risk values, allowing for easy comparison across tickers. This involves scaling the total risk to a range between 0 and 1.
   ```python
   risk_rating = (total_risk - total_risk.min()) / (total_risk.max() - total_risk.min())
   ```

## Skills

- **Programming Languages**: Proficient in Python for data analysis.
- **Libraries**: Familiarity with Pandas for data manipulation and analysis.
- **Data Analysis**: Ability to preprocess and analyze stock market data using statistical methods.

## Results & Business Recommendations

### Anomaly Detection Results

   ![Correlation Close Price](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/corr_close.png)
   ![Correlation Volume](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/corr_volume.png)

### Risk Assessment Metrics

   ![Risk Rating](https://github.com/VishShaji/Stock-Market-Anomaly-Detection/blob/main/media/risk_score.png)

Based on the findings, it is recommended that investors:

- Monitor identified anomalies closely to assess their impact on investment strategies.
- Consider using Z-score analysis as a straightforward method for real-time anomaly detection.
- Conduct further research on the causes of detected anomalies to enhance understanding and predictive capabilities.

## Next Steps

1. **Further Analysis**: Explore additional statistical methods for anomaly detection beyond Z-scores.
2. **Real-Time Implementation**: Develop a system for real-time anomaly detection using the Alpha Vantage API.
3. **User Training**: Create training materials for users to effectively interpret and act upon anomaly detection results.
4. **Expand Data Sources**: Consider incorporating alternative data sources (e.g., news sentiment analysis) to enrich the anomaly detection framework.
