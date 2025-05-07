# Timer and Date Mocks

<!-- - `jest.useFakeTimers()` / `jest.useRealTimers()`
- `jest.advanceTimersByTime(ms)`
- `jest.runAllTimers()`
- `jest.runOnlyPendingTimers()`
- `jest.setSystemTime(time)`
- `jest.clearAllTimers()`  -->

## Keyword Explanations

- `useFakeTimers()`: Replaces the real timer functions (setTimeout, setInterval, clearTimeout, clearInterval) with mock implementations. This allows you to control time in your tests.

- `useRealTimers()`: Restores the real timer functions after using fake timers.

- `advanceTimersByTime()`: Advances all timers by the specified number of milliseconds. This is useful for testing code that uses setTimeout or setInterval.

- `runAllTimers()`: Runs all pending timers immediately. This is useful when you want to test code that uses multiple timers.

- `runOnlyPendingTimers()`: Runs only the timers that are currently pending. This is useful when you want to test code that uses multiple timers but only want to run the ones that are currently scheduled.

- `setSystemTime()`: Sets the system time that will be returned by Date.now() and new Date(). This is useful for testing code that depends on the current time.

- `clearAllTimers()`: Removes all pending timers. This is useful for cleaning up after tests that use timers.

## Examples

```javascript
describe('Timer and Date Mocks', () => {
  beforeEach(() => {
    jest.useFakeTimers();
  });

  afterEach(() => {
    jest.useRealTimers();
  });

  // Example 1: Testing setTimeout
  it('handles setTimeout', () => {
    const callback = jest.fn();
    setTimeout(callback, 1000);
    
    expect(callback).not.toBeCalled();
    jest.advanceTimersByTime(1000);
    expect(callback).toBeCalled();
  });

  // Example 2: Testing setInterval
  it('handles setInterval', () => {
    const callback = jest.fn();
    setInterval(callback, 1000);
    
    expect(callback).not.toBeCalled();
    jest.advanceTimersByTime(1000);
    expect(callback).toBeCalledTimes(1);
    jest.advanceTimersByTime(1000);
    expect(callback).toBeCalledTimes(2);
  });

  // Example 3: Testing multiple timers
  it('handles multiple timers', () => {
    const callback1 = jest.fn();
    const callback2 = jest.fn();
    
    setTimeout(callback1, 1000);
    setTimeout(callback2, 2000);
    
    jest.runAllTimers();
    expect(callback1).toBeCalled();
    expect(callback2).toBeCalled();
  });

  // Example 4: Testing Date
  it('mocks Date', () => {
    const mockDate = new Date('2024-01-01');
    jest.setSystemTime(mockDate);
    
    expect(new Date().getTime()).toBe(mockDate.getTime());
    expect(Date.now()).toBe(mockDate.getTime());
  });

  // Example 5: Testing debounced function
  it('tests debounced function', () => {
    const debouncedFn = jest.fn();
    const debounce = (fn, delay) => {
      let timeoutId;
      return (...args) => {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => fn(...args), delay);
      };
    };
    
    const debounced = debounce(debouncedFn, 1000);
    debounced();
    debounced();
    debounced();
    
    expect(debouncedFn).not.toBeCalled();
    jest.runAllTimers();
    expect(debouncedFn).toBeCalledTimes(1);
  });
}); 
```