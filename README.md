# Builder Design Pattern Implementation

## Overview

The **Builder Design Pattern** is used to construct complex objects step-by-step, allowing for more readable and maintainable object creation. This diagram illustrates the creation of a `Hero` class using a builder approach, where properties such as armor, hair color, hair type, weapon, and profession are set incrementally.

![image](https://github.com/user-attachments/assets/a7953549-712c-43e5-9d71-a75265583c54)

---

## Class Diagram Explanation

### **Core Classes**

1. **`Hero`**:
   - **Purpose**: Represents the final product, a hero, with customizable properties.
   - **Attributes**:
     - `name`: The hero's name.
     - `profession`: The hero's profession (e.g., Mage, Warrior).
     - `armor`: The type of armor the hero wears (e.g., Chain Mail, Plate Mail).
     - `hairType`: The style of the hero's hair (e.g., Bald, Curly).
     - `hairColor`: The color of the hero's hair (e.g., Black, Red).
     - `weapon`: The hero's weapon of choice (e.g., Sword, Bow).
   - **Methods**:
     - `Hero(Builder builder)`: Constructor used by the builder to create a `Hero`.
     - Getter methods (`getName()`, `getArmor()`, etc.) for accessing attributes.
     - `toString()`: Provides a string representation of the hero's attributes.

2. **`Builder`**:
   - **Purpose**: Facilitates the step-by-step construction of a `Hero` object.
   - **Attributes**: Same as the `Hero` class but used as interim placeholders during the build process.
   - **Methods**:
     - `Builder(Profession profession, String name)`: Initializes a builder with required fields (`profession` and `name`).
     - `build()`: Constructs and returns a fully built `Hero` instance.
     - Fluent methods (`withArmor()`, `withHairColor()`, etc.) for setting optional attributes.

---

### **Enums**

1. **`Profession`**:
   - **Purpose**: Enumerates possible hero professions.
   - **Values**: `MAGE`, `PRIEST`, `THIEF`, `WARRIOR`.
   - **Methods**:
     - `toString()`: Returns a string representation of the profession.
     - Static methods for retrieving enum values (`valueOf()` and `values()`).

2. **`Armor`**:
   - **Purpose**: Enumerates possible types of armor.
   - **Values**: `CHAIN_MAIL`, `CLOTHES`, `LEATHER`, `PLATE_MAIL`.
   - **Methods**: Similar to the `Profession` enum.

3. **`HairColor`**:
   - **Purpose**: Enumerates possible hair colors.
   - **Values**: `BLACK`, `BLOND`, `BROWN`, `RED`, `WHITE`.
   - **Methods**: Similar to the `Profession` enum.

4. **`HairType`**:
   - **Purpose**: Enumerates possible hair types.
   - **Values**: `BALD`, `CURLY`, `LONG_CURLY`, `LONG_STRAIGHT`, `SHORT`.
   - **Methods**: Similar to the `Profession` enum.

5. **`Weapon`**:
   - **Purpose**: Enumerates possible weapons.
   - **Values**: `AXE`, `BOW`, `DAGGER`, `SWORD`, `WARHAMMER`.
   - **Methods**: Similar to the `Profession` enum.

---

### **Relationships**

1. **`Hero` and `Builder`**:
   - `Hero` is constructed using the `Builder` class. The `Hero` class depends on the `Builder` for its instantiation (`Builder ..+ Hero`).

2. **`Hero` and Enums**:
   - The `Hero` class has attributes for `Profession`, `Armor`, `HairColor`, `HairType`, and `Weapon`, all defined as enums (`Hero --> -attribute Enum`).

3. **`Builder` and Enums**:
   - The `Builder` class provides methods for setting values for the `Hero` attributes (`Builder --> -attribute Enum`).

---

## How It Works

1. **Step-by-Step Construction**:
   - The client initializes a `Builder` with required attributes: `Profession` and `name`.
   - Additional attributes (e.g., `Armor`, `HairColor`, `Weapon`) are set using fluent methods (`withArmor()`, `withHairColor()`).

2. **Building the Object**:
   - The `build()` method is called to create a `Hero` instance. The `Hero` constructor uses the `Builder` to initialize all attributes.

3. **Example Usage**:
   ```java
   Hero hero = new Builder(Profession.WARRIOR, "Aragorn")
                   .withArmor(Armor.PLATE_MAIL)
                   .withHairColor(HairColor.BROWN)
                   .withHairType(HairType.LONG_STRAIGHT)
                   .withWeapon(Weapon.SWORD)
                   .build();

   System.out.println(hero);
   ```

---

## Advantages of Using the Builder Pattern

- **Readable and Maintainable Code**: Constructs complex objects with clear and fluent APIs.
- **Immutable Objects**: The `Hero` object is immutable after construction.
- **Scalability**: Easy to add new attributes or configuration options to the `Hero` without affecting client code.
