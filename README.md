```javascript
// Project: Product Inventory Management System

// 1. Data and Input Initialization

const inventory = [
    { id: 1, name: "Laptop", price: 55000 },
    { id: 2, name: "Mouse", price: 500 },
    { id: 3, name: "Keyboard", price: 1500 },
    { id: 4, name: "Monitor", price: 12000 }
];

// Taking input from the user
let productName = prompt("Enter the new product name:");
let productPrice = Number(prompt("Enter the product price:"));

// 2. Control Flow and Conditional Evaluation

if (
    productName === null ||
    productName.trim() === "" ||
    !Number.isFinite(productPrice) ||
    productPrice <= 0
) {
    console.log("Invalid input! Please enter a valid name and price.");
} else {
    // Adding a new product
    inventory.push({
        id: inventory.length + 1,
        name: productName.trim(),
        price: productPrice
    });

    console.log("Product added successfully!");

    // Assigning category using switch
    function getCategory(price) {
        let category;

        switch (true) {
            case price < 1000:
                category = "Budget";
                break;

            case price < 10000:
                category = "Standard";
                break;

            default:
                category = "Premium";
        }

        return category;
    }

    // 3. Loops and Flow Control

    console.log("\\nSearching inventory...");

    for (let i = 0; i < inventory.length; i++) {
        if (!inventory[i].name) {
            continue;
        }

        if (inventory[i].name.toLowerCase() ===
            productName.trim().toLowerCase()) {
            console.log("Product found:", inventory[i].name);
            break;
        }
    }

    // 4. Functions and Scope

    // Regular function to calculate total inventory value
    function calculateTotal(items) {
        let total = 0;

        for (let item of items) {
            total += item.price;
        }

        return total;
    }

    // Arrow function to calculate tax
    const calculateTax = (price, taxRate = 18) => {
        return price * taxRate / 100;
    };

    // Arrow function to calculate discount
    const calculateDiscount = (price, discountRate = 10) => {
        return price * discountRate / 100;
    };

    // 5. Array Methods and Iteration

    console.log("\\n========== INVENTORY SHEET ==========");

    // forEach(): Display all products
    inventory.forEach(function (item) {
        console.log(
            "ID:", item.id,
            "| Name:", item.name,
            "| Price: ₹" + item.price,
            "| Category:", getCategory(item.price)
        );
    });

    // filter(): Find products costing less than ₹10,000
    const budgetProducts = inventory.filter(
        item => item.price < 10000
    );

    console.log("\\nProducts below ₹10,000:");

    budgetProducts.forEach(item => {
        console.log(item.name + " - ₹" + item.price);
    });

    // map(): Create a transformed report
    const report = inventory.map(item => ({
        productName: item.name,
        originalPrice: item.price,
        tax: calculateTax(item.price),
        discount: calculateDiscount(item.price),
        finalPrice:
            item.price +
            calculateTax(item.price) -
            calculateDiscount(item.price),
        category: getCategory(item.price)
    }));

    console.log("\\n========== FINAL REPORT ==========");

    console.table(report);

    // Display total inventory statistics
    console.log("\\nTotal Products:", inventory.length);
    console.log("Total Inventory Value: ₹" + calculateTotal(inventory));

    // Display highest-priced product
    let highest = inventory[0];

    for (const item of inventory) {
        if (item.price > highest.price) {
            highest = item;
        }
    }

    console.log(
        "Highest-Priced Product:",
        highest.name,
        "- ₹" + highest.price
    );
}
```

**Note:** Run this program in a browser environment because `prompt()` is a browser function. Open the browser's developer console to see the output. The tax and discount are calculated independently on the original price, using an 18% tax rate and a 10% discount by default.
