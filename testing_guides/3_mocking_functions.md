# Mocking Functions

<!-- ## Creating Mocks
- `jest.fn()` – create mock function
- `vi.fn()` – Vitest version
- `jest.mock(path, factory?)` – auto-mock modules
- `vi.mock(path, factory?)`

## Mock Matchers
- `.toHaveBeenCalled()`
- `.toHaveBeenCalledTimes(number)`
- `.toHaveBeenCalledWith(...args)`
- `.toHaveBeenLastCalledWith(...args)`
- `.toHaveBeenNthCalledWith(n, ...args)`
- `.toHaveReturned()`
- `.toHaveReturnedWith(value)`
- `.toHaveLastReturnedWith(value)`  -->

## Keyword Explanations

### Creating Mocks
- `jest.fn()`: Creates a new mock function. The mock function can track calls, arguments, and return values.
- `vi.fn()`: Vitest's version of `jest.fn()`, works the same way but for Vitest testing framework.
- `jest.mock()`: Automatically mocks a module. All exports from the module will be mocked.
- `vi.mock()`: Vitest's version of `jest.mock()`, works the same way but for Vitest.

### Mock Matchers
- `toHaveBeenCalled()`: Verifies that the mock function was called at least once.
- `toHaveBeenCalledTimes()`: Verifies that the mock function was called exactly n times.
- `toHaveBeenCalledWith()`: Verifies that the mock function was called with specific arguments.
- `toHaveBeenLastCalledWith()`: Verifies the arguments of the most recent call to the mock function.
- `toHaveBeenNthCalledWith()`: Verifies the arguments of the nth call to the mock function.
- `toHaveReturned()`: Verifies that the mock function has returned a value at least once.
- `toHaveReturnedWith()`: Verifies that the mock function has returned a specific value.
- `toHaveLastReturnedWith()`: Verifies the return value of the most recent call to the mock function.

## Examples

```javascript
// Example 1: Basic Mock Function
describe('Basic Mock Function', () => {
  const mockFn = jest.fn();
  
  it('tracks calls and arguments', () => {
    mockFn('hello', 'world');
    mockFn('goodbye');
    
    expect(mockFn).toHaveBeenCalled();
    expect(mockFn).toHaveBeenCalledTimes(2);
    expect(mockFn).toHaveBeenCalledWith('hello', 'world');
    expect(mockFn).toHaveBeenLastCalledWith('goodbye');
  });
});

// Example 2: Mock with Return Value
describe('Mock with Return Value', () => {
  const mockCalculator = jest.fn()
    .mockReturnValue(42)
    .mockReturnValueOnce(10)
    .mockReturnValueOnce(20);
  
  it('returns different values on subsequent calls', () => {
    expect(mockCalculator()).toBe(10);  // First call
    expect(mockCalculator()).toBe(20);  // Second call
    expect(mockCalculator()).toBe(42);  // All subsequent calls
    expect(mockCalculator).toHaveReturnedWith(42);
  });
});

// Example 3: Mock Implementation
describe('Mock Implementation', () => {
  const mockFetch = jest.fn().mockImplementation((url) => {
    if (url.includes('error')) {
      return Promise.reject('Network error');
    }
    return Promise.resolve({ data: 'success' });
  });
  
  it('handles different scenarios', async () => {
    const success = await mockFetch('api/success');
    expect(success).toEqual({ data: 'success' });
    
    await expect(mockFetch('api/error')).rejects.toBe('Network error');
  });
});

// Example 4: Module Mocking
// userService.js
export const getUser = (id) => fetch(`/api/users/${id}`);

// userService.test.js
jest.mock('./userService', () => ({
  getUser: jest.fn().mockResolvedValue({ id: 1, name: 'John' })
}));

describe('Module Mocking', () => {
  it('uses mocked module', async () => {
    const user = await getUser(1);
    expect(user).toEqual({ id: 1, name: 'John' });
  });
}); 
```