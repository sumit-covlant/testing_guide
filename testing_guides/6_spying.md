# Spying

<!-- - `jest.spyOn(object, methodName)`
- `vi.spyOn(object, methodName)`  -->

## Keyword Explanations

- `jest.spyOn()`: Creates a spy on a method of an object. A spy is a special type of mock that allows you to track calls to a method while still executing the original implementation. This is useful when you want to verify that a method was called without changing its behavior.

- `vi.spyOn()`: Vitest's version of `jest.spyOn()`, works the same way but for Vitest testing framework. It creates a spy that can track method calls while preserving the original implementation.

## Examples

```javascript
// Example 1: Basic Spying
describe('Basic Spying', () => {
  const calculator = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b
  };

  it('spies on method calls', () => {
    const addSpy = jest.spyOn(calculator, 'add');
    
    calculator.add(2, 3);
    expect(addSpy).toHaveBeenCalledWith(2, 3);
    expect(addSpy).toHaveReturnedWith(5);
  });
});

// Example 2: Spying on Class Methods
class User {
  constructor(name) {
    this.name = name;
  }
  
  getName() {
    return this.name;
  }
  
  setName(name) {
    this.name = name;
  }
}

describe('Spying on Class Methods', () => {
  let user;
  let getNameSpy;
  
  beforeEach(() => {
    user = new User('John');
    getNameSpy = jest.spyOn(user, 'getName');
  });
  
  it('tracks method calls while preserving behavior', () => {
    expect(user.getName()).toBe('John');
    expect(getNameSpy).toHaveBeenCalled();
    expect(getNameSpy).toHaveReturnedWith('John');
  });
});

// Example 3: Spying on Object Methods
describe('Spying on Object Methods', () => {
  const math = {
    sum: (...numbers) => numbers.reduce((a, b) => a + b, 0),
    average: (...numbers) => math.sum(...numbers) / numbers.length
  };
  
  it('spies on interdependent methods', () => {
    const sumSpy = jest.spyOn(math, 'sum');
    
    const result = math.average(1, 2, 3);
    expect(result).toBe(2);
    expect(sumSpy).toHaveBeenCalledWith(1, 2, 3);
  });
});

// Example 4: Spying on Console Methods
describe('Spying on Console Methods', () => {
  it('tracks console.log calls', () => {
    const consoleSpy = jest.spyOn(console, 'log');
    
    console.log('Hello, World!');
    expect(consoleSpy).toHaveBeenCalledWith('Hello, World!');
    
    consoleSpy.mockRestore(); // Restore original console.log
  });
});

// Example 5: Spying on Async Methods
describe('Spying on Async Methods', () => {
  const api = {
    async fetchData() {
      return { data: 'test' };
    }
  };
  
  it('spies on async method calls', async () => {
    const fetchSpy = jest.spyOn(api, 'fetchData');
    
    const result = await api.fetchData();
    expect(result).toEqual({ data: 'test' });
    expect(fetchSpy).toHaveBeenCalled();
    expect(fetchSpy).toHaveReturnedWith(Promise.resolve({ data: 'test' }));
  });
});
``` 