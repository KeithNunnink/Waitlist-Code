# Waitlist Code
 waitlist project code (final)
import time   # Import the time function so we can track times

class Waitlist:
    def __init__(self):   #use of __init__- an instance method that initializes the newly created "self" or any other object set
        self.waitlist = {}

    def add_to_waitlist(self, name):   #creates add to waitlist function
        if name not in self.waitlist:
            self.waitlist[name] = time.time()     #time.time() is from our time import
            print(f"{name} has been added to the waitlist.") #utilization of the F string to create expressions inside the brackets
        else:
            print(f"{name} is already on the waitlist.")

    def remove_from_waitlist(self, name):   #created remove from waitlist function
        if name in self.waitlist:
            wait_time = time.time() - self.waitlist[name]
            del self.waitlist[name]     #removes name from waitlist
            print(f"{name} has been removed from the waitlist. Wait time: {wait_time:.2f} seconds.")
            return wait_time
        else:
            print(f"{name} is not on the waitlist.")    #example of error handling
            return None

    def get_wait_time(self, name):  #create function for getting the wait time
        if name in self.waitlist:
            wait_time = time.time() - self.waitlist[name]
            print(f"{name} has been waiting for {wait_time:.2f}  seconds.")   #instruction to print the time
            return wait_time
        else:
            print(f"{name} is not on the waitlist.")    #error control here. if name isnt on waitlist
            return None


    def average_wait_time(self):   #create a function to find the average of wait times
        if len(self.waitlist) == 0:
            print("No one is on the waitlist.")   #output if waitlist is empty
            return None
        total_wait_time = sum(time.time() - wait_time for wait_time in self.waitlist.values())    #math to find average wait time
        avg_wait_time = total_wait_time / len(self.waitlist)
        print(f"Average wait time: {avg_wait_time:.2f}  seconds.")   #display wait time average in console
        return avg_wait_time

    def display_waitlist(self):   # create function that shows the entire wait list with name and time on there
        if len(self.waitlist) == 0:
            print("Waitlist is empty.")
        else:
            print("Waitlist:")
            for name, wait_time in self.waitlist.items():
                print(f"{name}: {time.time() - wait_time:.2f} seconds")

def main():         #
    waitlist = Waitlist()      #creates the actual waitlist for use

    while True:  #created a WHILE loop for user prompt in the console
        print("\nWaitlist Options:")
        print("1. Add to waitlist")
        print("2. Remove from waitlist")   #these are the prompts in the console
        print("3. Check wait time")
        print("4. Show average wait time")
        print("5. Display waitlist")
        print("6. Exit")

        choice = input("Enter your choice: ")   #create a variable for choice to ask user for input

        if choice == '1':
            name = input("Enter name to add to waitlist: ")
            waitlist.add_to_waitlist(name)
        elif choice == '2':
            name = input("Enter name to remove from waitlist: ")
            waitlist.remove_from_waitlist(name)
        elif choice == '3':
            name = input("Enter name to check wait time: ")
            waitlist.get_wait_time(name)
        elif choice == '4':
            waitlist.average_wait_time()    #These are all the options for the user to choose from in the console
        elif choice == '5':
            waitlist.display_waitlist()
        elif choice == '6':
            print("Exiting program.")
            break   #Break nested under final ELIF so there is a way to exit the loop
        else:
            print("Invalid choice. Please try again.")   #error control, if someone enters an invalid input

if __name__ == "__main__":
    main()
