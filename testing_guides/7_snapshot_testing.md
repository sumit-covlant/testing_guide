# Snapshot Testing

<!-- - `expect(value).toMatchSnapshot()`
- `expect(value).toMatchInlineSnapshot()`  -->

## Keyword Explanations

- `toMatchSnapshot()`: Creates a snapshot of the value and compares it with previously stored snapshots. If no snapshot exists, it creates one. This is useful for testing the structure of complex objects or UI components.

- `toMatchInlineSnapshot()`: Similar to `toMatchSnapshot()` but stores the snapshot inline in the test file. This makes it easier to review and update snapshots as they're right next to the test code.

## Examples

```javascript
// Example 1: Basic Snapshot Testing
describe('Basic Snapshot Testing', () => {
  it('matches snapshot of object', () => {
    const user = {
      name: 'John Doe',
      age: 30,
      email: 'john@example.com',
      address: {
        street: '123 Main St',
        city: 'New York',
        country: 'USA'
      }
    };
    
    expect(user).toMatchSnapshot();
  });
});

// Example 2: Inline Snapshot Testing
describe('Inline Snapshot Testing', () => {
  it('matches inline snapshot of object', () => {
    const config = {
      apiUrl: 'https://api.example.com',
      timeout: 5000,
      retries: 3
    };
    
    expect(config).toMatchInlineSnapshot();
  });
});

// Example 3: Snapshot Testing with React Components
// Button.jsx
const Button = ({ text, onClick }) => (
  <button onClick={onClick} className="btn">
    {text}
  </button>
);

// Button.test.jsx
describe('Button Component', () => {
  it('matches snapshot', () => {
    const button = render(<Button text="Click me" onClick={() => {}} />);
    expect(button).toMatchSnapshot();
  });
});

// Example 4: Snapshot Testing with Dynamic Content
describe('Dynamic Content Snapshot Testing', () => {
  it('matches snapshot with dynamic date', () => {
    const message = {
      text: 'Hello',
      timestamp: new Date('2024-01-01').toISOString(),
      id: Math.random().toString(36).substr(2, 9)
    };
    
    // Use a custom snapshot serializer to handle dynamic values
    expect(message).toMatchSnapshot({
      timestamp: expect.any(String),
      id: expect.any(String)
    });
  });
});

// Example 5: Snapshot Testing with Error Messages
describe('Error Message Snapshot Testing', () => {
  it('matches error message snapshot', () => {
    const error = new Error('Invalid input');
    error.code = 'INVALID_INPUT';
    error.details = {
      field: 'email',
      message: 'Must be a valid email address'
    };
    
    expect(error).toMatchSnapshot();
  });
}); 
```