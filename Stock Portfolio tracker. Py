# CodeAlpha_task-3
import yfinance as yf
import pandas as pd
portfolio = {}
# To Fetch stock data using yfinance
def get_stock_data(tickers):
    stock_data = yf.download(tickers, period="1d")['Adj Close']
    return stock_data
# Calculate portfolio value and performance
def calculate_portfolio_value(portfolio, stock_data):
    total_value = 0
    portfolio_summary = []

    for stock, shares in portfolio.items():
        current_price = stock_data[stock].values[0]
        stock_value = current_price * shares
        total_value += stock_value

        portfolio_summary.append({
            'Stock': stock,
            'Shares': shares,
            'Current Price': round(current_price, 2),
            'Total Value': round(stock_value, 2)
        })

    return total_value, portfolio_summary

# Display the portfolio
def display_portfolio(portfolio):
    if not portfolio:
        print("Your portfolio is currently empty.")
        return
    
    tickers = list(portfolio.keys())
    stock_data = get_stock_data(tickers)
    total_value, portfolio_summary = calculate_portfolio_value(portfolio, stock_data)
    
    df = pd.DataFrame(portfolio_summary)
    print("\nPortfolio Summary:\n")
    print(df)
    print(f"\nTotal Portfolio Value: ${round(total_value, 2)}")

# Add or update a stock in the portfolio
def add_or_update_stock(portfolio):
    stock = input("Enter stock ticker symbol (e.g., AAPL): ").upper()
    shares = int(input(f"Enter number of shares for {stock}: "))
    
    if stock in portfolio:
        portfolio[stock] += shares
        print(f"Updated {stock} with {shares} additional shares. Now you own {portfolio[stock]} shares.")
    else:
        portfolio[stock] = shares
        print(f"Added {stock} to your portfolio with {shares} shares.")

# To Remove a stock
def remove_stock(portfolio):
    stock = input("Enter stock ticker symbol to remove (e.g., AAPL): ").upper()
    
    if stock in portfolio:
        del portfolio[stock]
        print(f"Removed {stock} from your portfolio.")
    else:
        print(f"{stock} not found in your portfolio.")

# Track portfolio performance
def track_performance(portfolio):
    if not portfolio:
        print("Your portfolio is currently empty.")
        return
    
    tickers = list(portfolio.keys())
    # Fetch stock data for the last 6 months
    stock_data = yf.download(tickers, period="6mo")['Adj Close']

    print("\nStock Performance Over the Last 6 Months:\n")
    print(stock_data)

# Main function to interact with the user
def manage_portfolio(portfolio):
    while True:
        print("\n--- Portfolio Management ---")
        print("1. View Portfolio")
        print("2. Add or Update Stock")
        print("3. Remove Stock")
        print("4. Track Stock Performance (6 Months)")
        print("5. Exit")
        
        choice = input("Choose an option (1-5): ")
        
        if choice == '1':
            display_portfolio(portfolio)
        elif choice == '2':
            add_or_update_stock(portfolio)
        elif choice == '3':
            remove_stock(portfolio)
        elif choice == '4':
            track_performance(portfolio)
        elif choice == '5':
            print("Exiting portfolio manager.")
            break
        else:
            print("Invalid choice, please try again.")

# To run
manage_portfolio(portfolio)
