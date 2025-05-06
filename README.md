#include <stdio.h>
#include <string.h>

#define MAX_ITEMS 100

typedef struct {
    int id;
    char name[50];
    float price;
    int quantity;
} Item;

typedef struct {
    Item items[MAX_ITEMS];
    int count;
} Cart;

// Function to add item to cart
void addItem(Cart *cart) {
    if (cart->count >= MAX_ITEMS) {
        printf("Cart is full!\n");
        return;
    }
    Item item;
    printf("Enter item ID: ");
    scanf("%d", &item.id);

   printf("Enter item name: ");
    scanf(" %[^\n]s", item.name);  // space before %[^\n]s to consume newline

   printf("Enter item price: ");
    scanf("%f", &item.price);
    printf("Enter quantity: ");
    scanf("%d", &item.quantity);
    cart->items[cart->count++] = item;
    printf("Item added to cart!\n");
}
// Function to display cart
void displayCart(const Cart *cart) {
    if (cart->count == 0) {
        printf("Cart is empty.\n");
        return;
    }
    float total = 0.0;
    printf("\n--- Shopping Cart ---\n");
    for (int i = 0; i < cart->count; i++) {
        Item item = cart->items[i];
        float itemTotal = item.price * item.quantity;
        printf("%d. %s - $%.2f x %d = $%.2f\n", i + 1, item.name, item.price, item.quantity, itemTotal);
        total += itemTotal;
    }
    printf("Total Amount: $%.2f\n\n", total);
}
// Main function
int main() {
    Cart myCart = {.count = 0};
    int choice;
    while (1) {
        printf("----- Online Shopping Cart -----\n");
        printf("1. Add Item\n");
        printf("2. View Cart\n");
        printf("3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
       switch (choice) {
            case 1:
                addItem(&myCart);
                break;
            case 2:
                displayCart(&myCart);
                break;
            case 3:
                printf("Thank you for shopping!\n");
                return 0;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }
}
