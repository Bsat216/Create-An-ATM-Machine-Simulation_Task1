class ATM:
    def __init__(self, balance=1000, pin="1234"):
        self.balance = balance
        self.pin = pin

    def authenticate(self):
        attempts = 0
        while attempts < 3:
            entered_pin = input("Enter your PIN: ")
            if entered_pin == self.pin:
                print("Authentication successful!\n")
                return True
            else:
                print("Incorrect PIN. Try again.\n")
                attempts += 1
        print("Too many incorrect attempts. Card blocked.")
        return False

    def display_menu(self):
        print("\n----- ATM MENU -----")
        print("1. Check Balance")
        print("2. Deposit")
        print("3. Withdraw")
        print("4. Exit")

    def check_balance(self):
        print(f"Your current balance is: ${self.balance:.2f}")

    def deposit(self):
        try:
            amount = float(input("Enter amount to deposit: $"))
            if amount > 0:
                self.balance += amount
                print(f"Deposited ${amount:.2f}. New balance is ${self.balance:.2f}.")
            else:
                print("Deposit amount must be positive.")
        except ValueError:
            print("Invalid input. Please enter a numeric value.")

    def withdraw(self):
        try:
            amount = float(input("Enter amount to withdraw: $"))
            if 0 < amount <= self.balance:
                self.balance -= amount
                print(f"Withdrew ${amount:.2f}. New balance is ${self.balance:.2f}.")
            elif amount > self.balance:
                print("Insufficient balance.")
            else:
                print("Withdrawal amount must be positive.")
        except ValueError:
            print("Invalid input. Please enter a numeric value.")

    def run(self):
        if not self.authenticate():
            return
        while True:
            self.display_menu()
            choice = input("Choose an option (1-4): ")
            if choice == '1':
                self.check_balance()
            elif choice == '2':
                self.deposit()
            elif choice == '3':
                self.withdraw()
            elif choice == '4':
                print("Thank you for using the ATM. Goodbye!")
                break
            else:
                print("Invalid selection. Please try again.")

# Run the ATM simulation
atm = ATM()
atm.run()
