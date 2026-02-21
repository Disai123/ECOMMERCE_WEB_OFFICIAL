# Testing Guide - Aishani E-commerce

This document outlines the testing strategy, stages, and instructions for the Aishani E-commerce platform.

## 🧪 Testing Stages

### 1. Unit Testing
Focuses on individual components, hooks, and utility functions in isolation.
- **Tools**: Jest, React Testing Library.
- **Location**: `__tests__/components/*` and alongside source files.

### 2. Integration Testing
Verifies that multiple parts of the system work together (e.g., Pages interacting with hooks/Store).
- **Location**: `__tests__/pages/*`.

### 3. API & Data Testing
Verifies Prisma schemas and API route logic.
- **Tools**: Jest (with Prisma mocking).

---

## 🚀 How to Run Tests

### Run All Tests
```bash
npm test
```

### Watch Mode (Development)
```bash
npm run test:watch
```

### Coverage Report
Generates a detailed HTML report of which lines are covered by tests.
```bash
npm run test:coverage
```

---

## 📂 Directory Structure

```text
__tests__/
├── components/      # Unit tests for UI components (e.g., Button, Input)
└── pages/           # Integration tests for Next.js pages
```

---

## ✅ Best Practices

1. **Mock External Services**: Always mock Stripe, Cloudinary, and Prisma in unit tests.
2. **Test User Interactions**: Prefer testing what the user sees (labels, roles) over internal implementation details.
3. **Keep Tests Atomic**: Each test should focus on a single behavior.
