# billing-Software
import datetime

class BillingSoftware:
    def __init__(self):
        self.items = []  # Each item will be stored as a dict

    def add_item(self, name, price, quantity):
        self.items.append({
            "name": name,
            "price": price,
            "quantity": quantity,
            "total": price * quantity
        })

    def generate_bill(self):
        if not self.items:
            print("\nNo items in the cart!")
            return

        print("\n====== BILL ======")
        print("Date:", datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
        print("-------------------")
        subtotal = 0
        for item in self.items:
            print(f"{item['name']} (x{item['quantity']}) - ₹{item['total']:.2f}")
            subtotal += item["total"]

        tax = subtotal * 0.18  # 18% GST
        total = subtotal + tax

        print("-------------------")
        print(f"Subtotal: ₹{subtotal:.2f}")
        print(f"Tax (18%): ₹{tax:.2f}")
        print(f"Total: ₹{total:.2f}")
        print("===================")

        # Save to file
        filename = f"Bill_{datetime.datetime.now().strftime('%Y%m%d_%H%M%S')}.txt"
        with open(filename, "w") as f:
            f.write("===== CUSTOMER BILL =====\n")
            f.write("Date: " + datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S") + "\n\n")
            for item in self.items:
                f.write(f"{item['name']} (x{item['quantity']}) - ₹{item['total']:.2f}\n")
            f.write("\n-------------------\n")
            f.write(f"Subtotal: ₹{subtotal:.2f}\n")
            f.write(f"Tax (18%): ₹{tax:.2f}\n")
            f.write(f"Total: ₹{total:.2f}\n")
        print(f"\nBill saved as {filename}")

    def reset(self):
        self.items = []
        print("\nSystem reset for next customer!\n")


# -------------------------------
# Main Program
# -------------------------------
def main():
    software = BillingSoftware()

    while True:
        print("\n=== Billing Software ===")
        print("1. Add Item")
        print("2. Generate Bill")
        print("3. Reset")
        print("4. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            name = input("Enter item name: ")
            try:
                price = float(input("Enter item price: ₹"))
                quantity = int(input("Enter quantity: "))
                software.add_item(name, price, quantity)
                print(f"{quantity} x {name} added!")
            except ValueError:
                print("Invalid input! Price must be number, quantity must be integer.")
        elif choice == "2":
            software.generate_bill()
        elif choice == "3":
            software.reset()
        elif choice == "4":
            print("Exiting Billing Software. Goodbye!")
            break
        else:
            print("Invalid choice, try again.")


if __name__ == "__main__":
    main()

