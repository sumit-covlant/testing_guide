# Assertions (expect) and Matchers

<!-- ## Basic Matchers
- `expect(value).toBe(value)`
- `expect(value).toEqual(value)` – deep equality
- `expect(value).toStrictEqual(value)` – strict deep equality
- `expect(value).not.toBe(value)` – negation

## Numbers & Comparisons
- `toBeGreaterThan(number)`
- `toBeGreaterThanOrEqual(number)`
- `toBeLessThan(number)`
- `toBeLessThanOrEqual(number)`
- `toBeCloseTo(number, numDigits?)`

## Truthiness
- `toBeTruthy()`
- `toBeFalsy()`
- `toBeNull()`
- `toBeUndefined()`
- `toBeDefined()`
- `toBeNaN()`

## Objects & Arrays
- `toContain(item)` – for arrays/strings
- `toContainEqual(object)` – deep match in array
- `toHaveLength(length)`
- `toHaveProperty(path, value?)`
- `toMatchObject(object)`
- `toMatch(regexp|string)`

## Errors
- `toThrow(error?)`
- `toThrowError(error?)` -->

## Keyword Explanations

### Basic Matchers
- `expect`: The main assertion function that starts every test assertion.
- `toBe`: Tests exact equality using `Object.is()`.
- `toEqual`: Performs deep equality check, comparing all properties recursively.
- `toStrictEqual`: Like `toEqual` but also checks for undefined properties and type equality.
- `not`: Inverts the following matcher's result.

### Numbers & Comparisons
- `toBeGreaterThan`: Checks if a number is greater than the expected value.
- `toBeGreaterThanOrEqual`: Checks if a number is greater than or equal to the expected value.
- `toBeLessThan`: Checks if a number is less than the expected value.
- `toBeLessThanOrEqual`: Checks if a number is less than or equal to the expected value.
- `toBeCloseTo`: Checks if a number is close to the expected value, useful for floating-point comparisons.

### Truthiness
- `toBeTruthy`: Checks if a value is truthy (evaluates to true in a boolean context).
- `toBeFalsy`: Checks if a value is falsy (evaluates to false in a boolean context).
- `toBeNull`: Checks if a value is exactly null.
- `toBeUndefined`: Checks if a value is undefined.
- `toBeDefined`: Checks if a value is not undefined.
- `toBeNaN`: Checks if a value is NaN.

### Objects & Arrays
- `toContain`: Checks if an array or string contains a specific item or substring.
- `toContainEqual`: Checks if an array contains an object that matches the expected object.
- `toHaveLength`: Checks if an array or string has a specific length.
- `toHaveProperty`: Checks if an object has a specific property, optionally with a specific value.
- `toMatchObject`: Checks if an object contains a subset of the expected object's properties.
- `toMatch`: Checks if a string matches a regular expression or contains a substring.

### Errors
- `toThrow`: Checks if a function throws an error when called.
- `toThrowError`: Like `toThrow` but also checks the error message or type.

## Examples

```javascript
describe('Assertion Examples', () => {
  // Basic Matchers
  it('basic equality checks', () => {
    expect(2 + 2).toBe(4);
    expect({ name: 'John' }).toEqual({ name: 'John' });
    expect({ name: 'John', age: undefined }).toStrictEqual({ name: 'John' });
    expect(2 + 2).not.toBe(5);
  });

  // Numbers & Comparisons
  it('number comparisons', () => {
    const value = 10;
    expect(value).toBeGreaterThan(5);
    expect(value).toBeLessThan(20);
    expect(0.1 + 0.2).toBeCloseTo(0.3, 5); // Handles floating point precision
  });

  // Truthiness
  it('truthiness checks', () => {
    expect(true).toBeTruthy();
    expect(false).toBeFalsy();
    expect(null).toBeNull();
    expect(undefined).toBeUndefined();
    expect(0).toBeDefined();
    expect(NaN).toBeNaN();
  });

  // Objects & Arrays
  it('object and array checks', () => {
    const shoppingList = ['milk', 'bread', 'eggs'];
    expect(shoppingList).toContain('milk');
    expect(shoppingList).toHaveLength(3);
    
    const user = { name: 'John', age: 30 };
    expect(user).toHaveProperty('name');
    expect(user).toMatchObject({ name: 'John' });
    expect('Hello World').toMatch(/World/);
  });

  // Errors
  it('error handling', () => {
    function throwError() {
      throw new Error('Something went wrong');
    }
    
    expect(() => throwError()).toThrow();
    expect(() => throwError()).toThrowError('Something went wrong');
  });
}); 
```