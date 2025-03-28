From this [problem I try to solve on exercism](https://exercism.org/tracks/cpp/exercises/eliuds-eggs) I get an interested discussion, open my ayes to bitwise operators.

# Bitwise Operations in C++

Bitwise operations manipulate individual bits of integers. C++ provides **six bitwise operators**:

| Operator | Name                        | Example |
|----------|-----------------------------|---------|
| `&`      | Bitwise AND                 | `x & y` |
| `|`      | Bitwise OR                  | `x | y` |
| `^`      | Bitwise XOR                 | `x ^ y` |
| `~`      | Bitwise NOT (Complement)     | `~x`    |
| `<<`     | Left Shift                   | `x << n` |
| `>>`     | Right Shift                   | `x >> n` |

---

## Bitwise AND (`&`)
Performs a **bitwise AND** operation on corresponding bits of two numbers. **Only `1 & 1` results in `1`, everything else is `0`.**

### Example
```cpp
int x = 5;  // 0101
int y = 3;  // 0011
int result = x & y; // 0001 (1 in decimal)
```
### Use Cases:
- Masking specific bits  
- Checking if a number is even/odd (`x & 1 == 0` for even)

---

## Bitwise OR (`|`)
Performs a **bitwise OR** operation. **If at least one bit is `1`, the result is `1`.**

### Example
```cpp
int x = 5;  // 0101
int y = 3;  // 0011
int result = x | y; // 0111 (7 in decimal)
```
### Use Cases:  
- Combining bit masks

---

## Bitwise XOR (`^`)
Performs an **exclusive OR** operation. **If bits are different, the result is `1`, otherwise it's `0`.**

### **Example**
```cpp
int x = 5;  // 0101
int y = 3;  // 0011
int result = x ^ y; // 0110 (6 in decimal)
```
### Use Cases:
- **Swapping two numbers without extra variable:**
  ```cpp
  int a = 5, b = 3;
  a = a ^ b; // 0101 ^ 0011 = 0110 (6)
  b = a ^ b; // 0110 ^ 0011 = 0101 (5)
  a = a ^ b; // 0110 ^ 0101 = 0011 (3)
  ```
- Finding the unique element in an array where every other element appears twice.

---

## Bitwise NOT (`~`)
Flips all bits (**1 → 0, 0 → 1**). This is a **one's complement** operation.

### **Example**
```cpp
int x = 5;   // 0000 0101
int result = ~x; // 1111 1010  (Two's complement form for -6)
```
### Caution:  
`~x` is **not** simply `-x`, it's actually `-(x+1)` in signed integers due to two's complement representation.

### Use Cases:  
- Finding the negative of a number (`~x + 1` is `-x`)  
- Flipping bits in low-level programming

---

## Left Shift (`<<`)
Shifts all bits to the **left** by `n` positions. **Fills right with `0`s.**

### **Example**
```cpp
int x = 5;   // 0000 0101
int result = x << 1; // 0000 1010 (10 in decimal)
```
- **Equivalent to multiplying by `2^n`**  
### **Use Cases:**  
- Fast multiplication by powers of 2 (`x << 3` = `x * 8`)  
- Bit manipulation tricks

---

## Right Shift (`>>`)
Shifts all bits to the **right** by `n` positions.

### **Example**
```cpp
int x = 5;   // 0000 0101
int result = x >> 1; // 0000 0010 (2 in decimal)
```
- **Equivalent to integer division by `2^n`**  
### Use Cases:  
- Fast division by powers of 2 (`x >> 2` = `x / 4`)  
- Extracting individual bits

- **For signed integers, behavior depends on compiler (logical vs arithmetic shift).**  

---

## Summary Table
| Operator | Effect                     | Equivalent To |
|----------|----------------------------|--------------|
| `x & y`  | Bitwise AND                | -            |
| `x | y`  | Bitwise OR                 | -            |
| `x ^ y`  | Bitwise XOR                 | -            
| `~x`     | Bitwise NOT                 | `-(x+1)` (for signed) |
| `x << n` | Left shift (multiply by `2^n`) | `x * (2^n)` |
| `x >> n` | Right shift (divide by `2^n`) | `x / (2^n)` |

---

## **Bonus: Checking if a Number is a Power of 2**
```cpp
bool isPowerOf2(int x) {
    return (x > 0) && ((x & (x - 1)) == 0);
}
``