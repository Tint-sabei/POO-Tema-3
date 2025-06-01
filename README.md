# POO-Tema-3

# Project 3: Feeding Hungry Cat Game

## Overview

This C++ project is an interactive cat-feeding simulation that demonstrates advanced Object-Oriented Programming (OOP), templates, and design patterns. The game allows users to create different types of cats (Domestic, Fat, Stray), feed them various foods, and track their status through a user-friendly menu.

---

## Template Requirements 

### Function Template

```cpp
template<typename T>
void displayInfo(const T& item);
```

* Located in `GameUtils.hpp`.
* Used to show food treatment and eating animation for any food type.

### Class Template / T Usage

```cpp
template<typename CatType>
void addGenericCat(GameState& game, const std::string& name, int age, int fullness);
```

* This template function allows flexible addition of any `Cat` subtype.

* The `T` type is also indirectly involved in the smart pointer instantiation, fulfilling the requirement for using `T` in a parameter and inside a method.

---

## Design Patterns

### Singleton Pattern – `GameState`

```cpp
static GameState& getInstance();
```

* A private constructor prevents multiple instances.
* Ensures centralized game management.
* *Chosen because*: It guarantees consistent game logic and shared access to all cat data.

### Strategy Pattern – Feeding Behavior

```cpp
class FeedingStrategy { virtual int getFullnessIncrease() const = 0; };
class NormalFeeding : public FeedingStrategy { ... };
class FatCatFeeding : public FeedingStrategy { ... };
```

* Applied when feeding cats: different behavior for `FatCat` and others.
* *Chosen because*: It separates feeding logic from cat classes and makes it easy to extend behavior for new cat types in the future.

### Factory Method Pattern – Food Creation

```cpp
static std::shared_ptr<Food> createFish();
static std::shared_ptr<Food> createDryFood();
static std::shared_ptr<Food> createMilk();
```

* Static methods in `Food` create different types of food.
* *Chosen because*: It encapsulates object creation and lets the game logic focus on "what to create" without knowing "how."

---

## Example Run

```
1. Show Cats
2. Add Cat
3. Feed Cat
4. Total Cats
5. Cat Sound
6. Exit
Choice: 1
[0] Domestic Cat - Mimi, Age: 3, Fullness: 80
[1] Fat Cat - Chonky, Age: 5, Fullness: 60
[2] Stray Cat - Ghost, Age: 2, Fullness: 40
```

---

## Notes

* Avoid overfeeding: fullness level > 100 triggers `FullnessTooHighException`.
* The code is modular and demonstrates safe memory management using `shared_ptr`.
* Templates and design patterns are used meaningfully, not just for compliance.
