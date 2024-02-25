class RestoranAyamGoreng:
    def __init__(self):
        self.menu = {}
        self.menu_id_counter = 1
        
    def create_menu_item(self, name, price, description):
        menu_id = len(self.menu) + 1
        self.menu[menu_id] = {'name': name, 'price': price, 'description': description}
        return menu_id

    def read_menu_item(self, menu_id):
        return self.menu.get(menu_id, "Menu item not found.")

    def update_menu_item(self, menu_id, name=None, price=None, description=None):
        if menu_id in self.menu:
            menu_item = self.menu[menu_id]
            if name:
                menu_item['name'] = name
            if price:
                menu_item['price'] = price
            if description:
                menu_item['description'] = description
            return "Menu item updated successfully."
        else:
            return "Menu item not found."

    def delete_menu_item(self, menu_id):
        if menu_id in self.menu:
            del self.menu[menu_id]
            return "Menu item deleted successfully."
        else:
            return "Menu item not found."
        
def display_menu(restaurant):
    if restaurant.menu:
        print("Menu:")
        for menu_id, menu_item in restaurant.menu.items():
            print(f"ID: {menu_id}, Name: {menu_item['name']}, Price: {menu_item['price']}, Description: {menu_item['description']}")
    else:
        print("Menu is empty.")
        
def menu():
    print("\nMenu:")
    print("1. Add Menu")
    print("2. View Menu")
    print("3. Update Menu")
    print("4. Delete Menu")
    print("5. Exit")
    return input("Choice Menu: ")

# Main program
print ("Welcome To Ayam Pedas Menyala Abangkuh")

restaurant = RestoranAyamGoreng()
while True:
    choice = menu()
    if choice == '1':
        try:
         name = input("Enter menu name: ")
         price = int(input("Enter menu price: "))
         description = input("Enter menu description: ")
         menu_id = restaurant.create_menu_item(name, price, description)
         print("Menu added with ID:", menu_id)
        except ValueError:
            print("Menu invalid, check again")
    elif choice == '2':
         display_menu(restaurant)
    elif choice == '3':
        try:
         menu_id = int(input("Enter menu ID to update: "))

         name = input("Enter new menu name (leave empty to skip): ")
         price = int(input("Enter new menu price (leave 0 to skip): "))
         description = input("Enter new menu description (leave empty to skip): ")
         print(restaurant.update_menu_item(menu_id, name, price, description))
        except ValueError:
            print("Menu invalid, check again")
    elif choice == '4':
        try:
         menu_id = int(input("Enter menu ID to delete: "))
         print(restaurant.delete_menu_item(menu_id))
        except ValueError:
            print("Menu invalid, check again")
    elif choice == '5':
        print("Exiting program...")
        break
    else:
        print("Invalid choice. Please try again.")
