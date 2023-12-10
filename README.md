class Appointment:
    def __init__(self, day_of_week, start_time_hour):
        self.client_name = ""
        self.client_phone = ""
        self.appt_type = 0  # Representing an available appointment by default
        self.day_of_week = day_of_week
        self.start_time_hour = start_time_hour

    def get_appt_type_desc(self):
        appt_types = {
            0: "Available",
            1: "Men's Cut $50",
            2: "Ladies Cut $80",
            3: "Men's Colouring $50",
            4: "Ladies Colouring $120"
        }
        return appt_types.get(self.appt_type, "Invalid Appointment Type")

    def __str__(self):
        return f"{self.client_name}   {self.client_phone}   {self.day_of_week}   {self.start_time_hour:02d}:00 - {self.start_time_hour + 1:02d}:00   {self.get_appt_type_desc()}"

def create_weekly_calendar():
    appointments = []
    for day in ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]:
        for hour in range(9, 17):
            appointments.append(Appointment(day, hour))
    return appointments

def display_available_slots(appointments):
    print("\nAvailable Appointment Slots:")
    for appointment in appointments:
        if appointment.appt_type == 0:
            print(appointment)

def get_client_name():
    return input("Enter your name: ")

def get_client_phno():
    return input("Enter your phone number: ")

def get_app_type():
    print("╔══════════════════════════════════════════╗")
    print("║        Available Appointment Types       ║")
    print("╠══════════════════════════════════════════╣")
    print("║  0 - Available                           ║")
    print("║  1 - Men's cut                           ║")
    print("║  2 - Ladies cut                          ║")
    print("║  3 - Men's coloring                      ║")
    print("║  4 - Ladies coloring                     ║")
    print("╚══════════════════════════════════════════╝")
    return int(input("Enter your choice: "))


def cancel(appointments):
    client_name = input("Enter client name: ")
    for appointment in appointments:
        if appointment.client_name == client_name:
            print(f"{client_name}'s appointment is canceled")
            appointments.remove(appointment)
            break
    else:
        print(f"{client_name} is not registered")

def day_of_week_input():
    return input("Enter the day of the week: ")

def start_time_input():
    return int(input("Enter the start time (hour): "))

def show_appointments_by_name(appointments, client_name):
        matching_appointments = [
            appointment for appointment in appointments
            if client_name.lower() in appointment.client_name.lower()
        ]
        
        if matching_appointments:
            print(f"Appointments for '{client_name}':")
            for appointment in matching_appointments:
                print(appointment)
        else:
            print(f"No appointments found for '{client_name}'.")
            
def show_appointments_by_day(appointments, day_to_show):
    matching_appointments = [
        appointment for appointment in appointments
        if appointment.day_of_week.lower() == day_to_show.lower()
    ]
    
    if matching_appointments:
        print(f"Appointments for '{day_to_show}':")
        for appointment in matching_appointments:
            print(appointment)
    else:
        print(f"No appointments found for '{day_to_show}'.")

def main():
    appointments = []

    while True:
        print("***********************************************")
        print("Welcome To Jojo's Hair Salon")
        print("***********************************************")
        print("1 - Book an appointment")
        print("2 - Cancel an appointment")
        print("3 - Find appointment by name")
        print("4 - Find appoinment by day")
        print("5 - Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            day_of_week = day_of_week_input()
            start_time_hour = start_time_input()

            appointment = Appointment(day_of_week, start_time_hour)
            appointment.client_name = get_client_name()
            appointment.client_phone = get_client_phno()
            appointment.appt_type = get_app_type()

            appointments.append(appointment)
            print("Appointment booked successfully!")
            print(appointment)

        elif choice == "2":
            cancel(appointments)
            
        elif choice == "3":
            client_name = input("Enter client's name: ")
            show_appointments_by_name(appointments, client_name)
            
        elif choice == "4":
            day_to_show = input("Enter the day of the week: ")
            show_appointments_by_day(appointments, day_to_show)

        elif choice == "5":
            print("Exiting program.")
            break

        else:
            print("Invalid choice. Please enter 1, 2, 3, or 4.")
        
        print("Please press Enter to continue...")
        input()  # wait for Enter key 

if __name__ == "__main__":
    main()
