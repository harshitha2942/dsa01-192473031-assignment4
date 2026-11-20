# Task 6 – Design challenge: vehicle rental fleet

## Stage 1 – Requirements
Entities: Vehicle, Bicycle, MotorVehicle, TwoWheeler, Car, ElectricCar and RentalFleet. Common data: registration and daily rate. Motor-specific data: fuel/charge level and service due date. Car data: seat capacity. Electric car data: battery capacity. Behaviour that varies: rental charge and type-specific details.

Testable requirements:
1. Fleet can store and list multiple concrete vehicle types through base pointers.
2. A vehicle cannot be rented twice without being returned.
3. Daily rental cost is daily rate multiplied by rental days.
4. Fuel vehicles add a per-litre charge; electric vehicles add a per-kWh charge.
5. Returning a vehicle changes its state to available.
6. A new type can be added without editing fleet iteration or the Vehicle interface.

## Stage 2 – Hierarchy
```text
                 Vehicle (abstract)
                 /               \
            Bicycle          MotorVehicle
                             /     |      \
                       TwoWheeler  Car  ElectricCar

New extension: ElectricBus : MotorVehicle
```
`Vehicle` is abstract because `charge()` and `type()` are pure virtual. Inheritance is public. MotorVehicle is an intermediate class containing shared motor-specific state.

## Stage 3/4 – Decisions and pseudocode
- `charge`, `type` and destructor are virtual; concrete charge implementations override the base contract.
- Fleet owns `unique_ptr<Vehicle>` in a vector.
- Pseudocode:
```text
RENT(vehicle):
    IF vehicle is already rented THEN
        RETURN failure
    SET rented = true
    RETURN success

RETURN_VEHICLE(vehicle, lateDays):
    IF vehicle is not rented THEN
        RETURN failure
    SET rented = false
    lateCharge = lateDays * lateRate
    RETURN lateCharge
```
This demonstration uses a fixed late fee of Rs 200 in `main`; a production design would put the late-fee policy into a dedicated return method.

## Stage 5 – Demonstration
The program creates and lists a bicycle, two-wheeler, car, electric car and a newly added electric bus. It rents and returns a car, displays a late-fee calculation and computes an electric usage charge.

## Alternative: one Vehicle class and switch
A type-code design stores fields for all vehicle types and branches in `charge()`. Both a switch and virtual call are O(1) per charge. The single class has unused fields for many instances; polymorphic objects may carry a vptr (implementation-dependent). Adding a type requires editing the type code, switch, fields, creation and possibly listing logic. With an abstract base class, add a derived class and its factory/registration point; existing fleet processing remains unchanged.

## Required evidence
Compile with `g++ -std=c++17 -Wall -Wextra -pedantic`, run every task, save terminal screenshots, and record your actual compiler version. Add further tests for duplicate rental, returning a vehicle not rented, late return, and each concrete charge rule.
