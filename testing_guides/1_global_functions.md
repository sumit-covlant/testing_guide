# Global Functions

<!-- ## Test Definitions

- `describe(name, fn)` – group related tests
- `it(name, fn)` or `test(name, fn)` – define a single test case
- `beforeEach(fn)` / `afterEach(fn)` – setup/teardown per test
- `beforeAll(fn)` / `afterAll(fn)` – setup/teardown for the suite  -->

## Keyword Explanations

- `describe`: A function that groups related test cases together. It helps organize tests into logical units and provides a way to describe what feature or component is being tested.

- `it`/`test`: These are aliases of each other. They define individual test cases. The name parameter should describe what the test is checking, and the function parameter contains the actual test code.

- `beforeEach`: A function that runs before each test case in the current describe block. Useful for setting up test data or resetting state between tests.

- `afterEach`: A function that runs after each test case in the current describe block. Useful for cleaning up resources or resetting state after tests.

- `beforeAll`: A function that runs once before all test cases in the current describe block. Useful for one-time setup operations.

- `afterAll`: A function that runs once after all test cases in the current describe block. Useful for one-time cleanup operations.

## Examples

```javascript
// Example of a test suite for a calculator
describe('Calculator', () => {
  let calculator;
  
  // Runs once before all tests
  beforeAll(() => {
    console.log('Setting up calculator tests');
  });
  
  // Runs before each test
  beforeEach(() => {
    calculator = new Calculator();
  });
  
  // Runs after each test
  afterEach(() => {
    calculator = null;
  });
  
  // Runs once after all tests
  afterAll(() => {
    console.log('Cleaning up calculator tests');
  });
  
  // Individual test cases
  it('should add two numbers correctly', () => {
    expect(calculator.add(2, 3)).toBe(5);
  });
  
  it('should subtract two numbers correctly', () => {
    expect(calculator.subtract(5, 3)).toBe(2);
  });
  
  // Another way to write a test
  test('should multiply two numbers correctly', () => {
    expect(calculator.multiply(4, 3)).toBe(12);
  });
}); 
```