import json
import os

FILE_NAME = "boarding_passes.json"


# Load data from file
def load_data():
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    return []


# Save data to file
def save_data(data):
    with open(FILE_NAME, "w") as file:
        json.dump(data, file, indent=4)


# Create Boarding Pass
def create_pass():
    data = load_data()

    passenger_id = input("Enter Passenger ID: ")
    passenger_name = input("Enter Passenger Name: ")
    flight_no = input("Enter Flight Number: ")
    source = input("Enter Source: ")
    destination = input("Enter Destination: ")
    seat_no = input("Enter Seat Number: ")
    gate_no = input("Enter Gate Number: ")

    boarding_pass = {
        "Passenger ID": passenger_id,
        "Passenger Name": passenger_name,
        "Flight Number": flight_no,
        "Source": source,
        "Destination": destination,
        "Seat Number": seat_no,
        "Gate Number": gate_no
    }

    data.append(boarding_pass)
    save_data(data)

    print("\nBoarding Pass Created Successfully!")


# Display All Boarding Passes
def display_passes():
    data = load_data()

    if not data:
        print("\nNo Records Found!")
        return

    print("\n----- Boarding Pass Records -----")
    for bp in data:
        print("\nPassenger ID:", bp["Passenger ID"])
        print("Passenger Name:", bp["Passenger Name"])
        print("Flight Number:", bp["Flight Number"])
        print("Source:", bp["Source"])
        print("Destination:", bp["Destination"])
        print("Seat Number:", bp["Seat Number"])
        print("Gate Number:", bp["Gate Number"])
        print("-" * 35)


# Search Boarding Pass
def search_pass():
    data = load_data()

    pid = input("Enter Passenger ID to Search: ")

    for bp in data:
        if bp["Passenger ID"] == pid:
            print("\nBoarding Pass Found")
            for key, value in bp.items():
                print(f"{key}: {value}")
            return

    print("Record Not Found!")


# Update Boarding Pass
def update_pass():
    data = load_data()

    pid = input("Enter Passenger ID to Update: ")

    for bp in data:
        if bp["Passenger ID"] == pid:
            bp["Passenger Name"] = input("Enter New Passenger Name: ")
            bp["Seat Number"] = input("Enter New Seat Number: ")
            bp["Gate Number"] = input("Enter New Gate Number: ")

            save_data(data)
            print("Record Updated Successfully!")
            return

    print("Record Not Found!")


# Delete Boarding Pass
def delete_pass():
    data = load_data()

    pid = input("Enter Passenger ID to Delete: ")

    for bp in data:
        if bp["Passenger ID"] == pid:
            data.remove(bp)
            save_data(data)
            print("Record Deleted Successfully!")
            return

    print("Record Not Found!")


# Generate Boarding Pass
def generate_boarding_pass():
    data = load_data()

    pid = input("Enter Passenger ID: ")

    for bp in data:
        if bp["Passenger ID"] == pid:
            print("\n")
            print("=" * 50)
            print("         FLIGHT BOARDING PASS")
            print("=" * 50)
            print(f"Passenger Name : {bp['Passenger Name']}")
            print(f"Passenger ID   : {bp['Passenger ID']}")
            print(f"Flight Number  : {bp['Flight Number']}")
            print(f"From           : {bp['Source']}")
            print(f"To             : {bp['Destination']}")
            print(f"Seat Number    : {bp['Seat Number']}")
            print(f"Gate Number    : {bp['Gate Number']}")
            print("=" * 50)
            return

    print("Record Not Found!")


# Main Menu
while True:
    print("\n===== Flight Boarding Pass Generator =====")
    print("1. Create Boarding Pass")
    print("2. View All Boarding Passes")
    print("3. Search Boarding Pass")
    print("4. Update Boarding Pass")
    print("5. Delete Boarding Pass")
    print("6. Generate Boarding Pass")
    print("7. Exit")

    choice = input("Enter Your Choice: ")

    if choice == "1":
        create_pass()
    elif choice == "2":
        display_passes()
    elif choice == "3":
        search_pass()
    elif choice == "4":
        update_pass()
    elif choice == "5":
        delete_pass()
    elif choice == "6":
        generate_boarding_pass()
    elif choice == "7":
        print("Thank You!")
        break
    else:
        print("Invalid Choice!")
