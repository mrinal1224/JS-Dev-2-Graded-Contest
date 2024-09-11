### Problem Statement: Designing a Class Architecture for a Parking Lot System

In this exercise, you will create a class architecture for a **Parking Lot System**. You are required to design a constructor function `ParkingLot` that represents the parking lot and specific vehicles like `Car` and `Motorcycle` that inherit from a base `Vehicle` constructor.

### Problem Description:

You need to implement the following functionality:

1. Create a constructor function `Vehicle` that takes the following parameters:
    - `type`: The type of the vehicle, like "Car" or "Motorcycle".
    - `licensePlate`: The license plate of the vehicle.

2. Each instance of a `Vehicle` should have a method:
    - `enterParking(spotNumber)`: This method assigns a parking spot to the vehicle.

3. Create a `ParkingLot` constructor function that takes the following parameters:
    - `capacity`: The total number of parking spots available in the parking lot.
    - `vehicles`: An array to hold the parked vehicles.
  
4. Each instance of a `ParkingLot` should have the following methods:
    - `parkVehicle(vehicle, spotNumber)`: This method parks the vehicle in the parking lot at the specified spot if the spot is available.
    - `removeVehicle(spotNumber)`: This method removes a vehicle from a parking spot.

5. Create two specific types of vehicles:
   - `Car`: Inherits from `Vehicle`. When a car is parked, it requires one parking spot.
   - `Motorcycle`: Inherits from `Vehicle`. A motorcycle also requires one parking spot.

### Additional Requirements:
- Use prototypal inheritance to ensure that `Car` and `Motorcycle` inherit from `Vehicle`.
- The parking lot should have a fixed capacity. If the capacity is full, an error should be thrown when trying to park a vehicle.
- Each vehicle should have a unique parking spot. If a spot is already taken, an error should be thrown.
- Removing a vehicle frees up the spot for another vehicle.

### Example Scenarios:
1. Create a `ParkingLot` with 3 parking spots and park a `Car` with license plate "XYZ123" in spot 1.
2. Park a `Motorcycle` with license plate "MOTO456" in spot 2.
3. Try to park another vehicle in spot 1 and handle the error.
4. Remove the `Car` from spot 1, and park another `Motorcycle` in that spot.

### Hints:
- You can track the parking spots using an array or an object where the key is the spot number, and the value is the vehicle parked at that spot.
- Use prototypal inheritance to make sure `Car` and `Motorcycle` inherit from `Vehicle`.
- Validate if a parking spot is available before parking a vehicle.

### Code Stub:
```javascript
function Vehicle(type, licensePlate) {
    this.type = type;
    this.licensePlate = licensePlate;
}

Vehicle.prototype.enterParking = function(spotNumber) {
    this.parkingSpot = spotNumber;
};

function ParkingLot(capacity) {
    this.capacity = capacity;
    this.vehicles = {};
}

ParkingLot.prototype.parkVehicle = function(vehicle, spotNumber) {
    if (Object.keys(this.vehicles).length >= this.capacity) {
        throw new Error("Parking lot is full");
    }
    if (this.vehicles[spotNumber]) {
        throw new Error("Spot is already taken");
    }
    this.vehicles[spotNumber] = vehicle;
    vehicle.enterParking(spotNumber);
};

ParkingLot.prototype.removeVehicle = function(spotNumber) {
    if (!this.vehicles[spotNumber]) {
        throw new Error("No vehicle in this spot");
    }
    delete this.vehicles[spotNumber];
};

function Car(licensePlate) {
    Vehicle.call(this, "Car", licensePlate);
}

Car.prototype = Object.create(Vehicle.prototype);
Car.prototype.constructor = Car;

function Motorcycle(licensePlate) {
    Vehicle.call(this, "Motorcycle", licensePlate);
}

Motorcycle.prototype = Object.create(Vehicle.prototype);
Motorcycle.prototype.constructor = Motorcycle;

// Test cases
const lot = new ParkingLot(3);
const car = new Car('XYZ123');
const motorcycle = new Motorcycle('MOTO456');

lot.parkVehicle(car, 1);  // Car parked in spot 1
lot.parkVehicle(motorcycle, 2);  // Motorcycle parked in spot 2

console.log(lot.vehicles);  // { '1': Car, '2': Motorcycle }

lot.removeVehicle(1);  // Car removed from spot 1
const newMotorcycle = new Motorcycle('MOTO789');
lot.parkVehicle(newMotorcycle, 1);  // Motorcycle parked in spot 1
console.log(lot.vehicles);  // { '1': Motorcycle, '2': Motorcycle }
```

### Solution Approach:
1. **Vehicle Constructor:** Define a generic `Vehicle` constructor that holds properties like `type` and `licensePlate`.
2. **Prototypal Inheritance:** Set up prototypal inheritance so `Car` and `Motorcycle` inherit from `Vehicle`.
3. **ParkingLot Constructor:** Define a `ParkingLot` constructor that initializes the capacity and an empty object to track parked vehicles.
4. **parkVehicle Method:** Implement logic to check for available parking spots and ensure vehicles are parked correctly. Handle errors when the lot is full or the spot is taken.
5. **removeVehicle Method:** Implement logic to remove a vehicle from a specific parking spot, freeing up the spot for other vehicles.
6. **Test Cases:** Test parking and removing vehicles, checking for errors when the lot is full or spots are occupied.

### Complete Solution:
```javascript
function Vehicle(type, licensePlate) {
    this.type = type;
    this.licensePlate = licensePlate;
}

Vehicle.prototype.enterParking = function(spotNumber) {
    this.parkingSpot = spotNumber;
};

function ParkingLot(capacity) {
    this.capacity = capacity;
    this.vehicles = {};
}

ParkingLot.prototype.parkVehicle = function(vehicle, spotNumber) {
    if (Object.keys(this.vehicles).length >= this.capacity) {
        throw new Error("Parking lot is full");
    }
    if (this.vehicles[spotNumber]) {
        throw new Error("Spot is already taken");
    }
    this.vehicles[spotNumber] = vehicle;
    vehicle.enterParking(spotNumber);
};

ParkingLot.prototype.removeVehicle = function(spotNumber) {
    if (!this.vehicles[spotNumber]) {
        throw new Error("No vehicle in this spot");
    }
    delete this.vehicles[spotNumber];
};

function Car(licensePlate) {
    Vehicle.call(this, "Car", licensePlate);
}

Car.prototype = Object.create(Vehicle.prototype);
Car.prototype.constructor = Car;

function Motorcycle(licensePlate) {
    Vehicle.call(this, "Motorcycle", licensePlate);
}

Motorcycle.prototype = Object.create(Vehicle.prototype);
Motorcycle.prototype.constructor = Motorcycle;

// Test cases
try {
    const lot = new ParkingLot(3);
    const car = new Car('XYZ123');
    const motorcycle = new Motorcycle('MOTO456');
    
    lot.parkVehicle(car, 1);  // Car parked in spot 1
    console.log(lot.vehicles);  // { '1': Car }

    lot.parkVehicle(motorcycle, 2);  // Motorcycle parked in spot 2
    console.log(lot.vehicles);  // { '1': Car, '2': Motorcycle }

    // Trying to park another vehicle in an occupied spot
    const anotherCar = new Car('ABC789');
    lot.parkVehicle(anotherCar, 1);  // Error: Spot is already taken
} catch (error) {
    console.log(error.message);
}

try {
    const lot = new ParkingLot(2);
    const car = new Car('XYZ123');
    const motorcycle = new Motorcycle('MOTO456');
    
    lot.parkVehicle(car, 1);  // Car parked in spot 1
    lot.parkVehicle(motorcycle, 2);  // Motorcycle parked in spot 2
    
    lot.removeVehicle(1);  // Car removed from spot 1
    console.log(lot.vehicles);  // { '2': Motorcycle }

    const newMotorcycle = new Motorcycle('MOTO789');
    lot.parkVehicle(newMotorcycle, 1);  // Motorcycle parked in spot 1
    console.log(lot.vehicles);  // { '1': Motorcycle, '2': Motorcycle }
} catch (error) {
    console.log(error.message);
}
```

### Test Cases:
1. `lot.parkVehicle(car, 1)`: Car parks in spot 1.
2. `lot.parkVehicle(motorcycle, 2)`: Motorcycle parks in spot 2.
3. Trying to park a vehicle in an already occupied spot throws `"Spot is already taken"`.
4. `lot.removeVehicle(1)`: Removes the car from spot 1.
5. Successfully parks a new motorcycle in the freed spot.