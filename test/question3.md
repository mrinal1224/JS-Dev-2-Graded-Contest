### Problem Statement

You are tasked with writing a function called `walletSystem`, which simulates a more advanced digital wallet system that supports multiple currencies. The `walletSystem` function will take an initial balance (an object where the keys are currency codes like `USD`, `EUR`, etc., and values are numbers representing amounts) as input and return an object with the following methods:

1. **addFunds(currency, amount)**: Adds the specified `amount` to the balance of the specified `currency`. If the currency does not exist in the wallet, initialize it with the given `amount`.
2. **spendFunds(currency, amount)**: Subtracts the specified `amount` from the balance of the specified `currency`, but only if the balance is sufficient for that currency. If the balance is insufficient for that currency, return a message: `"Insufficient balance in {currency}!"`.
3. **checkBalance(currency)**: Returns the current balance for the specified `currency`. If the currency is not available in the wallet, return a message: `"No balance available for {currency}!"`.
4. **convertFunds(fromCurrency, toCurrency, conversionRate)**: Converts the entire balance from one currency to another using the provided `conversionRate`. The `conversionRate` will be a multiplier, such that `conversionRate * fromCurrencyBalance = toCurrencyBalance`. After conversion, the balance in `fromCurrency` should be set to zero.

**Requirements**:
- The balances should be maintained privately within the closure of the `walletSystem` function. They should not be directly accessible or modifiable outside of the provided methods.
- The wallet's methods should be the only way to interact with or modify the balances.
- Conversion should correctly calculate the balances in both currencies.

### Solution Approach

The solution requires:
1. **Private balance**: Store the balances for multiple currencies within the closure of the `walletSystem` function using an object.
2. **Methods**: Return an object containing the methods to interact with the wallet’s balance.
3. **addFunds**: Either increment the balance for an existing currency or initialize it if the currency doesn’t exist.
4. **spendFunds**: Subtract the amount from the balance of the specified currency if sufficient funds exist, or return an error message.
5. **checkBalance**: Return the balance of the specified currency or an error message if the currency is not found.
6. **convertFunds**: Convert the balance of one currency to another using the given conversion rate and update the balances accordingly.

### Hints

1. Use closures to encapsulate the wallet’s balances for multiple currencies.
2. You will need to maintain an object where each key is a currency code and each value is the balance for that currency.
3. Be careful with currency conversion. After conversion, the original currency’s balance should be set to zero.

### Test Cases

```javascript
const myWallet = walletSystem({ USD: 100, EUR: 200 });

console.log(myWallet.checkBalance('USD'));  // Output: 100
myWallet.addFunds('USD', 50);
console.log(myWallet.checkBalance('USD'));  // Output: 150
console.log(myWallet.spendFunds('USD', 200)); // Output: "Insufficient balance in USD!"
myWallet.spendFunds('USD', 30);
console.log(myWallet.checkBalance('USD'));  // Output: 120

myWallet.addFunds('GBP', 300);
console.log(myWallet.checkBalance('GBP'));  // Output: 300

myWallet.convertFunds('EUR', 'USD', 1.2); 
console.log(myWallet.checkBalance('EUR'));  // Output: 0
console.log(myWallet.checkBalance('USD'));  // Output: 360
```

### Code Stub

```javascript
function walletSystem(initialBalances) {
    // Students will write their solution here.
}

// Test your solution with the test cases below:
const myWallet = walletSystem({ USD: 100, EUR: 200 });

console.log(myWallet.checkBalance('USD'));  // Expected Output: 100
myWallet.addFunds('USD', 50);
console.log(myWallet.checkBalance('USD'));  // Expected Output: 150
console.log(myWallet.spendFunds('USD', 200)); // Expected Output: "Insufficient balance in USD!"
myWallet.spendFunds('USD', 30);
console.log(myWallet.checkBalance('USD'));  // Expected Output: 120

myWallet.addFunds('GBP', 300);
console.log(myWallet.checkBalance('GBP'));  // Expected Output: 300

myWallet.convertFunds('EUR', 'USD', 1.2); 
console.log(myWallet.checkBalance('EUR'));  // Expected Output: 0
console.log(myWallet.checkBalance('USD'));  // Expected Output: 360
```

### Complete Solution

```javascript
function walletSystem(initialBalances) {
    let balances = { ...initialBalances }; // Private object storing the balance for multiple currencies

    return {
        addFunds(currency, amount) {
            if (!balances[currency]) {
                balances[currency] = 0; // Initialize if currency doesn't exist
            }
            balances[currency] += amount;
        },
        spendFunds(currency, amount) {
            if (!balances[currency]) {
                return `No balance available for ${currency}!`;
            }
            if (amount > balances[currency]) {
                return `Insufficient balance in ${currency}!`;
            }
            balances[currency] -= amount;
        },
        checkBalance(currency) {
            if (!balances[currency]) {
                return `No balance available for ${currency}!`;
            }
            return balances[currency];
        },
        convertFunds(fromCurrency, toCurrency, conversionRate) {
            if (!balances[fromCurrency]) {
                return `No balance available for ${fromCurrency}!`;
            }
            const convertedAmount = balances[fromCurrency] * conversionRate;
            if (!balances[toCurrency]) {
                balances[toCurrency] = 0;
            }
            balances[toCurrency] += convertedAmount;
            balances[fromCurrency] = 0; // Set the original currency's balance to zero after conversion
        }
    };
}

// Test your solution with the test cases below:
const myWallet = walletSystem({ USD: 100, EUR: 200 });

console.log(myWallet.checkBalance('USD'));  // Output: 100
myWallet.addFunds('USD', 50);
console.log(myWallet.checkBalance('USD'));  // Output: 150
console.log(myWallet.spendFunds('USD', 200)); // Output: "Insufficient balance in USD!"
myWallet.spendFunds('USD', 30);
console.log(myWallet.checkBalance('USD'));  // Output: 120

myWallet.addFunds('GBP', 300);
console.log(myWallet.checkBalance('GBP'));  // Output: 300

myWallet.convertFunds('EUR', 'USD', 1.2); 
console.log(myWallet.checkBalance('EUR'));  // Output: 0
console.log(myWallet.checkBalance('USD'));  // Output: 360
```

This version introduces multi-currency handling and conversion, adding complexity by requiring students to manage multiple balances and perform calculations based on exchange rates. It also deepens their understanding of closures and state management in JavaScript.