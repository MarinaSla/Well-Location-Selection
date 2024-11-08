# Well Location Selection

## Project Description

Imagine you are working for the mining company "GRGN" and need to decide where to drill a new well.

You are provided with oil samples from three regions, each containing 10,000 oil fields, where the quality of oil and the volume of reserves have been measured. Your task is to build a machine learning model that will help determine which region will yield the highest profit from extraction. You will also analyze the potential profit and risks using the *Bootstrap* technique.

### Steps for Location Selection:
- In the selected region, search for oil fields and determine feature values for each one;
- Build a model and estimate the volume of reserves;
- Select the oil fields with the highest estimated values. The number of fields depends on the company's budget and the cost of developing each well;
- Profit is the total sum of profits from the selected fields.

## Research Goal

The goal of this analysis is to determine which region will provide the highest profit for drilling new wells.

## Research Tasks:
- Build a machine learning model to predict oil reserves and identify the region with the highest potential profit.
- Analyze potential profit and risks using the *Bootstrap* technique.
- Propose the best region for well development.

## Initial Data

Geological survey data for three regions are provided in the following files:  
`/datasets/geo_data_0.csv`  
`/datasets/geo_data_1.csv`  
`/datasets/geo_data_2.csv`

Columns in the dataset:
- `id` — Unique identifier for each well.
- `f0`, `f1`, `f2` — Feature values for each well.
- `product` — Volume of reserves in the well (in thousands of barrels).

### Task Conditions:
- Only linear regression is used for model training (other models are not sufficiently predictable).
- 500 data points are investigated for each region, from which 200 of the best points are selected for development.
- The budget for well development in each region is 10 billion rubles.
- Current prices: One barrel of raw material generates 450 rubles of income, and the volume is given in thousands of barrels (i.e., 1 unit = 450,000 rubles).
- After risk assessment, only regions with a loss probability of less than 2.5% should be considered. Among those, the region with the highest average profit will be selected.

**Note**: The data used in this analysis is synthetic, and details about the contracts and characteristics of the oil fields are not disclosed.

## Conclusions

1. **Data Preparation**:  
   Data from three regions was loaded, cleaned (no missing or duplicate values), and analyzed. Relationships and correlations between features were explored. The data was then prepared for machine learning, with training and validation sets created and a pipeline for data scaling implemented.

2. **Model Training and Evaluation**:  
   Machine learning models were trained and evaluated for each region using linear regression.

    - **Model for Region 0**  
      - RMSE of the best model on cross-validation: 37.67  
      - Average predicted reserves for Region 0: 92.4 thousand barrels  
      - RMSE of the model on the validation set: 37.76

    - **Model for Region 1**  
      - RMSE of the best model on cross-validation: 0.89  
      - Average predicted reserves for Region 1: 68.7 thousand barrels  
      - RMSE of the model on the validation set: 0.89

    - **Model for Region 2**  
      - RMSE of the best model on cross-validation: 38.74  
      - Average predicted reserves for Region 2: 94.8 thousand barrels  
      - RMSE of the model on the validation set: 38.88

    The model for Region 1 showed the lowest error. The errors for Regions 0 and 2 were similar. Predicted reserves for all regions were very close to the actual average reserve values.

3. **Profit Calculation**:  
   The sufficient volume of raw materials for break-even well development was calculated as 111.11 thousand barrels. In all regions, the predicted volume was lower than the sufficient volume for break-even development (Region 1 was significantly lower).  

    - Average reserves for Region 0: 92.5 thousand barrels  
    - Average reserves for Region 1: 68.83 thousand barrels  
    - Average reserves for Region 2: 95.0 thousand barrels  

    A function was created to calculate the profit from the selected wells and their predicted reserves. The top 200 wells were selected, the total predicted reserves were summed, and profit was calculated based on these reserves.

4. **Risk and Profit Analysis**:  
   Risks and profits were calculated for each region:

    - **Region 0**  
      - Average profit: 436,118,233 rubles  
      - 95% Confidence Interval of profit (negative profit is considered a loss): -116,231,613 to 966,504,181  
      - Probability of loss: 6.1%

    - **Region 1**  
      - Average profit: 489,661,254 rubles  
      - 95% Confidence Interval of profit: 55,116,177 to 905,762,650  
      - Probability of loss: 1.1%

    - **Region 2**  
      - Average profit: 603,514,836 rubles  
      - 95% Confidence Interval of profit: 85,659,911 to 1,153,069,187  
      - Probability of loss: 0.7%

    **Regions with a probability of loss less than 2.5%**: Region 1, Region 2

    **Recommendation**: For well development, **Region 2** is the most profitable choice, as it has the highest average profit among regions with a loss probability of less than 2.5%.


