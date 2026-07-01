# second-task
build a stock portfolio tracker. ● : ○ User inputs stock names and quantity. ○ Use a hardcoded dictionary to define stock prices (e.g., {"AAPL": 180, "TSLA": 250}). ○ Display total investment value and optionally save the result in a .txt or .csv file. ● Key Concepts Used: dictionary, input/output, basic arithmetic, file handling (optional).
# Stock Portfolio Tracker

import csv

# Hardcoded stock prices
stock_prices = {
    "AAPL": 180,
    "TSLA": 250,
    "GOOGL": 140,
    "MSFT": 330,
    "AMZN": 145
}

portfolio = {}
total_value = 0

print("=" * 40)
print("      STOCK PORTFOLIO TRACKER")
print("=" * 40)

print("\nAvailable Stocks:")
for stock, price in stock_prices.items():
    print(f"{stock} : ${price}")

# Number of stocks
n = int(input("\nHow many different stocks do you own? "))

# Input stock details
for i in range(n):
    stock = input(f"\nEnter Stock {i+1} Name: ").upper()

    if stock in stock_prices:
        quantity = int(input("Enter Quantity: "))
        portfolio[stock] = quantity
    else:
        print("Invalid Stock Name! Skipping...")

print("\n" + "=" * 55)
print("{:<10}{:<12}{:<12}{:<15}".format(
    "Stock", "Price($)", "Quantity", "Investment($)"
))
print("=" * 55)

# Calculate total investment
for stock, quantity in portfolio.items():
    investment = stock_prices[stock] * quantity
    total_value += investment

    print("{:<10}{:<12}{:<12}{:<15}".format(
        stock,
        stock_prices[stock],
        quantity,
        investment
    ))

print("=" * 55)
print(f"Total Portfolio Value = ${total_value}")
print("=" * 55)

# Save report
choice = input("\nDo you want to save the report? (yes/no): ").lower()

if choice == "yes":

    file_type = input("Save as txt or csv? ").lower()

    if file_type == "txt":

        with open("portfolio_report.txt", "w") as file:
            file.write("STOCK PORTFOLIO REPORT\n")
            file.write("=" * 40 + "\n")

            for stock, quantity in portfolio.items():
                investment = stock_prices[stock] * quantity

                file.write(
                    f"{stock} | Price: ${stock_prices[stock]} | "
                    f"Quantity: {quantity} | Investment: ${investment}\n"
                )

            file.write("\n")
            file.write(f"Total Portfolio Value = ${total_value}")

        print("Report saved as portfolio_report.txt")

    elif file_type == "csv":

        with open("portfolio_report.csv", "w", newline="") as file:
            writer = csv.writer(file)

            writer.writerow(
                ["Stock", "Price", "Quantity", "Investment"]
            )

            for stock, quantity in portfolio.items():
                investment = stock_prices[stock] * quantity

                writer.writerow([
                    stock,
                    stock_prices[stock],
                    quantity,
                    investment
                ])

            writer.writerow([])
            writer.writerow(["Total Portfolio Value", total_value])

        print("Report saved as portfolio_report.csv")

    else:
        print("Invalid file type.")

else:
    print("Report not saved.")

print("\nThank you for using the Stock Portfolio Tracker!") 

========================================
      STOCK PORTFOLIO TRACKER
========================================

Available Stocks:
AAPL : $180
TSLA : $250
GOOGL : $140
MSFT : $330
AMZN : $145

How many different stocks do you own? 3

Enter Stock 1 Name: AAPL
Enter Quantity: 5

Enter Stock 2 Name: TSLA
Enter Quantity: 2

Enter Stock 3 Name: MSFT
Enter Quantity: 4

=======================================================
Stock     Price($)    Quantity    Investment($)
=======================================================
AAPL      180         5           900
TSLA      250         2           500
MSFT      330         4           1320
=======================================================
Total Portfolio Value = $2720
=======================================================

Do you want to save the report? (yes/no): yes
Save as txt or csv? csv

Report saved as portfolio_report.csv

Thank you for using the Stock Portfolio Tracker!
