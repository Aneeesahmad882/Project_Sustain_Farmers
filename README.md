# Financial Insights Dashboard and Scoring Model
This project exposes a financial scoring model as a REST API using Flask. The API evaluates the financial health of families and individuals based on their income, expenses, savings, loan payments, and other financial factors. It provides a score (range 0–100) to assess financial stability.

Project Structure:
app.py: The main Flask application file, which exposes the /get_financial_score endpoint.
requirements.txt: File containing the necessary dependencies for running the app.
Setup Instructions
1. Clone or Download the Repository
Clone the repository or download the project files to your local machine.

2. Install Dependencies
Make sure you have Python installed. You can install the required Python packages using pip.

Run the following command in your project directory:
pip install -r requirements.txt

3. Run the Flask Application
To start the Flask API server, run the following command in your terminal:

python app.py
This will start the Flask server locally at http://127.0.0.1:5000/

4. Test the API
Once the server is running, you can test the API by sending a POST request to http://127.0.0.1:5000/get_financial_score with the appropriate input data.

5. Stopping the Server
To stop the server, press CTRL+C in the terminal where Flask is running.

Model Logic
The financial score is calculated based on the following factors:

1. Savings-to-Income Ratio
Formula:
Savings-to-Income Ratio
=
Savings
Income
Savings-to-Income Ratio= 
Income
Savings
​
 
Weight: This factor can contribute up to 50 points to the score.

2. Monthly Expenses-to-Income Ratio
Formula:
Expenses-to-Income Ratio
=
Monthly Expenses
Income
Expenses-to-Income Ratio= 
Income
Monthly Expenses
​
 
Weight: This factor can reduce up to 50 points from the score.

3. Loan Payments-to-Income Ratio
Formula:
Loan-to-Income Ratio
=
Loan Payments
Income
Loan-to-Income Ratio= 
Income
Loan Payments
​
 
Weight: This factor can reduce up to 30 points from the score.

4. Credit Card Spending
Formula:
Credit Card Spending Ratio
=
Credit Card Spending
Income
Credit Card Spending Ratio= 
Income
Credit Card Spending
​
 
Weight: This factor can reduce up to 20 points from the score.

5. Financial Goals Met
Formula: \text{Score Impact} = \text{Financial Goals Met (%)}
Weight: This factor can contribute up to 10 points to the score.
Final Score Calculation
The final financial score is calculated using the weighted sum of the factors. Here's how it is computed:

score = min(savings_to_income_ratio * 50, 50) - min(expenses_to_income_ratio * 50, 50) \
        - min(loan_to_income_ratio * 30, 30) - min(credit_card_spending_ratio * 20, 20) \
        + min(financial_goals_met_percentage * 0.5, 10)

## Ensure the score is between 0 and 100
score = max(0, min(score, 100))
