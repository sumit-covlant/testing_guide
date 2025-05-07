# Module Mocking

<!-- - `jest.mock()` / `vi.mock()`
- `jest.unmock()`
- `jest.doMock()` / `jest.dontMock()`
- `jest.resetModules()`  -->

## Keyword Explanations

- `jest.mock()`: Automatically mocks a module. All exports from the module will be mocked. This is useful when you want to replace a module's implementation with a mock version.

- `vi.mock()`: Vitest's version of `jest.mock()`, works the same way but for Vitest testing framework.

- `jest.unmock()`: Removes the mock implementation of a module, restoring its original implementation. This is useful when you want to use the real module in some tests.

- `jest.doMock()`: Similar to `jest.mock()` but can be called anywhere in the code. This is useful when you need to mock a module conditionally.

- `jest.dontMock()`: Similar to `jest.unmock()` but can be called anywhere in the code. This is useful when you need to unmock a module conditionally.

- `jest.resetModules()`: Resets the module registry, clearing all mocks. This is useful when you want to start fresh with module mocks between tests.

## Examples

```javascript
// Example 1: Basic Module Mocking
// math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// math.test.js
jest.mock('./math', () => ({
  add: jest.fn().mockReturnValue(42),
  subtract: jest.fn().mockReturnValue(21)
}));

describe('Basic Module Mocking', () => {
  it('uses mocked module', () => {
    const { add, subtract } = require('./math');
    expect(add(2, 2)).toBe(42);
    expect(subtract(10, 5)).toBe(21);
  });
});

// Example 2: Conditional Mocking
// userService.js
export const getUser = (id) => fetch(`/api/users/${id}`);

// userService.test.js
describe('Conditional Module Mocking', () => {
  it('uses real module', () => {
    jest.unmock('./userService');
    const { getUser } = require('./userService');
    // Uses real implementation
  });

  it('uses mocked module', () => {
    jest.mock('./userService', () => ({
      getUser: jest.fn().mockResolvedValue({ id: 1, name: 'John' })
    }));
    const { getUser } = require('./userService');
    // Uses mock implementation
  });
});

// Example 3: Dynamic Mocking
// config.js
export const getConfig = () => process.env.CONFIG;

// config.test.js
describe('Dynamic Module Mocking', () => {
  beforeEach(() => {
    jest.resetModules();
  });

  it('mocks module based on condition', () => {
    if (process.env.NODE_ENV === 'test') {
      jest.doMock('./config', () => ({
        getConfig: () => 'test-config'
      }));
    }
    const { getConfig } = require('./config');
    expect(getConfig()).toBe('test-config');
  });
});

// Example 4: Partial Module Mocking
// utils.js
export const formatDate = (date) => date.toISOString();
export const calculateAge = (birthDate) => {
  const today = new Date();
  return today.getFullYear() - birthDate.getFullYear();
};

// utils.test.js
jest.mock('./utils', () => {
  const originalModule = jest.requireActual('./utils');
  return {
    ...originalModule,
    formatDate: jest.fn().mockReturnValue('2024-01-01')
  };
});

describe('Partial Module Mocking', () => {
  it('mocks only specific functions', () => {
    const { formatDate, calculateAge } = require('./utils');
    expect(formatDate(new Date())).toBe('2024-01-01');
    expect(calculateAge(new Date('1990-01-01'))).toBe(34); // Real implementation
  });
}); 
```