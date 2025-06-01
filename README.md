# POO-Tema-3

# Project 3: Feeding Hungry Cat Game

## Overview

This C++ project is an interactive cat-feeding simulation that demonstrates advanced Object-Oriented Programming (OOP), templates, and design patterns. The game allows users to create different types of cats (Domestic, Fat, Stray), feed them various foods, and track their status through a user-friendly menu.

---

## Template Requirements

### Class Template: `StrayCat<T>`

```cpp
// StrayCat.hpp
template<typename T>
class StrayCat : public Cat {
private:
    T trait; // Attribute of type T

public:
    StrayCat() : Cat(), trait() {}
    StrayCat(std::string name, int age, int fullnessLevel)
        : Cat(name, age, fullnessLevel), trait() {}

    StrayCat(const StrayCat<T>& other) : Cat(other), trait(other.trait) {}
    StrayCat<T>& operator=(const StrayCat<T>& other) {
        if (this == &other) return *this;
        Cat::operator=(other);
        trait = other.trait;
        return *this;
    }

    std::shared_ptr<Cat> clone() const override {
        return std::make_shared<StrayCat<T>>(*this);
    }

    std::string getType() const override {
        return "Stray Cat";
    }

    void sound() const override {
        std::cout << "\nStray Cat Sound: HISSS!\n";
    }
};
```

### Attribute of Type T & `Member Function` Using T

```cpp
    // StrayCat.hpp
    void describeTrait() const {
        std::cout << "Trait info: " << trait << std::endl;
    }
```

### Function Template: `displayInfo<T>`

```cpp
// GameUtils.hpp
template<typename T>
void displayInfo(const T& item) {
    item.treat();
    item.eat();
}
```
* Used to display food treatment for any object having `treat()` and `eat()` methods.

### Free Function Template: `addGenericCat<T>`

```cpp
// GameUtils.hpp
template<typename CatType>
void addGenericCat(GameState& game, const std::string& name, int age, int fullness) {
    game.addCat(std::make_shared<CatType>(name, age, fullness));
}
```

* Allows flexible addition of any `Cat` subtype to the game using smart pointers.
---

## Design Patterns

### Singleton Pattern – `GameState`

```cpp
static GameState& getInstance();
```
* Ensures a single game manager handles all game state.
* **Why I used it**: My game logic depends on a shared list of cats and feeding actions. I needed a centralized, consistent controller to manage all interactions and data updates without conflict.




### Strategy Pattern – Feeding Behavior

```cpp
class FeedingStrategy { virtual int getFullnessIncrease() const = 0; };
class NormalFeeding : public FeedingStrategy { ... };
class FatCatFeeding : public FeedingStrategy { ... };
```

* Applied when feeding cats: different behavior for `FatCat` and others.
* **Why I used it**: Rather than hardcoding feeding behavior with conditions, I designed separate strategy classes that encapsulate each cat’s feeding logic. It makes the system easy to extend with new feeding rules.
  
### Factory Method Pattern – Food Creation

```cpp
static std::shared_ptr<Food> createFish();
static std::shared_ptr<Food> createDryFood();
static std::shared_ptr<Food> createMilk();
```

* Static methods in `Food` create different types of food.
* **Why I used it**: It allowed me to avoid `new` and to encapsulate food object creation logic in one place. Using smart pointers ensures there's no memory leak.
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
* Templates and design patterns are used meaningfully, not just for compliance.
