# COP2664-1-Lesson-8-Programming-Assignment
This repository link is a submission link for COP2664-1: Lesson 8 Programming Assignment

// This program is designed for a restaurant ordering system to calculate the total cost of the order the customer places.

import Foundation

protocol MenuItem {
    var name: String { get }
    var price: Double { get }
    func itemDescription() -> String
}
// This protocol defines the MenuItem protocol, which is used to define the MenuItem class.
class Food: MenuItem {
    var name: String
    var price: Double
    var cuisine: String
    init(name: String, price: Double, cuisine: String) {
        self.name = name
        self.price = price
        self.cuisine = cuisine
    }
    // This class defines the Food class, which is a subclass of MenuItem.
    func itemDescription() -> String {
        return "\(name) - $\(price) - \(cuisine)"
    }
}
class Beverage: MenuItem {
    var name: String
    var price: Double
    var isAlcoholic: Bool
    init(name: String, price: Double, isAlcoholic: Bool) {
        self.name = name
        self.price = price
        self.isAlcoholic = isAlcoholic
    }
    func itemDescription() -> String {
        return "\(name) - $\(price)"
    }
}
// This class defines the Beverage class, which is a subclass of MenuItem.
extension MenuItem {
    func calculateTax(rate: Double) -> Double {
        return price * rate
    }
}
// This extension defines the calculateTax method, which is used to calculate the tax on the price of the item.
class Order {
    var items: [MenuItem] = []
    func addItem(_item: MenuItem) {
        items.append(_item)
    }
    func calculateTotalCost() -> Double {
        var totalCost = 0.0
        for item in items {
            totalCost += item.price
        }
        return totalCost
    }
    func listItems() {
        for item in items {
            print(item.itemDescription())
        }
    }
}
// This class defines the Order class, which is used to create and manage the order.
enum OrderError: Error {
    case invalidItem
    case emptyOrder
    case invalidInput
}
// This enum defines the OrderError enum, which is used to represent errors that may occur during the order process.
func main() {
    let pasta = Food(name: "Chicken Alfredo", price: 14.99, cuisine: "Italian")
    let burger = Food(name: "Double Cheeseburger with Bacon", price: 10.95, cuisine: "American") 
    let soda = Beverage(name: "Coca-Cola", price: 3.99, isAlcoholic: false)
    let liquor = Beverage(name: "Coors Light", price: 2.49, isAlcoholic: true)
    // These lines create instances of the Food and Beverage classes, which are used to create MenuItem objects.
    let order = Order()
    order.addItem(_item: pasta)
    order.addItem(_item: burger)
    order.addItem(_item: soda)
    order.addItem(_item: liquor)
    // These lines add the MenuItem objects to the order.
    do {
        order.listItems()
        let totalCost = order.calculateTotalCost()
        print("Total cost: $\(totalCost)")
    } catch OrderError.invalidItem {
        print("Invalid item added to the order.")
    } catch OrderError.emptyOrder {
        print("The order is empty.")
    } catch OrderError.invalidInput {
        print("Invalid input.")
    }
}
// This function is the main function of the program. It creates an instance of the Order class, adds some MenuItem objects to the order, and then calculates and prints the total cost of the order.
main ()
