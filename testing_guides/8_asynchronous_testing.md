# Asynchronous Testing

<!-- - `await expect(promise).resolves.toEqual(value)`
- `await expect(promise).rejects.toThrow()`  -->

## Keyword Explanations

- `resolves`: A matcher that unwraps the value of a fulfilled promise and allows you to make assertions about that value. This is useful for testing asynchronous code that returns promises.

- `rejects`: A matcher that unwraps the reason of a rejected promise and allows you to make assertions about that reason. This is useful for testing error handling in asynchronous code.

- `toEqual`: When used with `resolves`, checks if the resolved value matches the expected value.

- `toThrow`: When used with `rejects`, checks if the rejected promise throws an error matching the expected error.

## Examples

```javascript
// Example 1: Basic Promise Testing
describe('Basic Promise Testing', () => {
  it('resolves with correct value', async () => {
    const promise = Promise.resolve(42);
    await expect(promise).resolves.toBe(42);
  });

  it('rejects with error', async () => {
    const promise = Promise.reject(new Error('Something went wrong'));
    await expect(promise).rejects.toThrow('Something went wrong');
  });
});

// Example 2: Testing Async Functions
describe('Async Function Testing', () => {
  const fetchUser = async (id) => {
    if (id === 1) {
      return { id: 1, name: 'John' };
    }
    throw new Error('User not found');
  };

  it('handles successful response', async () => {
    await expect(fetchUser(1)).resolves.toEqual({ id: 1, name: 'John' });
  });

  it('handles error response', async () => {
    await expect(fetchUser(999)).rejects.toThrow('User not found');
  });
});

// Example 3: Testing Multiple Async Operations
describe('Multiple Async Operations', () => {
  const fetchData = async () => {
    const [users, posts] = await Promise.all([
      fetch('/api/users'),
      fetch('/api/posts')
    ]);
    return { users, posts };
  };

  it('handles multiple promises', async () => {
    const result = await fetchData();
    expect(result).toHaveProperty('users');
    expect(result).toHaveProperty('posts');
  });
});

// Example 4: Testing Timeouts
describe('Timeout Testing', () => {
  const fetchWithTimeout = (url, timeout) => {
    return Promise.race([
      fetch(url),
      new Promise((_, reject) => 
        setTimeout(() => reject(new Error('Timeout')), timeout)
      )
    ]);
  };

  it('handles timeout', async () => {
    await expect(fetchWithTimeout('/api/slow', 1000))
      .rejects.toThrow('Timeout');
  });
});

// Example 5: Testing Async Error Handling
describe('Async Error Handling', () => {
  const validateUser = async (user) => {
    if (!user.name) {
      throw new Error('Name is required');
    }
    if (!user.email) {
      throw new Error('Email is required');
    }
    return true;
  };

  it('validates user data', async () => {
    const validUser = { name: 'John', email: 'john@example.com' };
    await expect(validateUser(validUser)).resolves.toBe(true);

    const invalidUser = { name: 'John' };
    await expect(validateUser(invalidUser))
      .rejects.toThrow('Email is required');
  });
}); 
```