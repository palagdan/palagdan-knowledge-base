# Fongard Industries Code Conventions

This document outlines the coding standards and best practices for TypeScript and JavaScript development at Fongard Industries. Our primary frameworks are **NestJS** for backend development and **React** for frontend development. Adhering to these conventions ensures consistency, maintainability, and scalability across our codebase.

## 1. General Principles
- **Consistency**: Follow these conventions across all projects to maintain a unified codebase.
- **Readability**: Write code that is easy to understand and maintain.
- **Modularity**: Break down code into reusable, single-responsibility components or modules.
- **Type Safety**: Leverage TypeScript's type system to catch errors early and improve code reliability.

## 2. File and Folder Structure
- **Backend (NestJS)**:
  - Organize modules by feature (e.g., `users`, `products`).
  - Use the following structure:
 
```
src/
├── modules/
│   ├── users/
│   │   ├── users.controller.ts
│   │   ├── users.service.ts
│   │   ├── users.module.ts
│   │   ├── dto/
YF    │   │   ├── entities/
│   │   └── interfaces/
├── shared/
│   ├── utils/
│   ├── config/
│   └── middleware/
└── main.ts
```

- **Frontend (React)**:
- Organize components by feature or page.
- Use the following structure:
```
src/
├── components/
│   ├── common/
│   ├── users/
│   └── products/
├── pages/
│   ├── UsersPage.tsx
│   └── ProductsPage.tsx
├── hooks/
├── services/
├── types/
├── utils/
└── App.tsx
```
- Use **kebab-case** for file and folder names (e.g., `user-profile.ts`).

## 3. Naming Conventions
- **Variables and Functions**: Use **camelCase** (e.g., `userProfile`, `fetchUserData`).
- **Classes and Interfaces**: Use **PascalCase** (e.g., `UserService`, `IUserProfile`).
- **Constants**: Use **UPPER_SNAKE_CASE** (e.g., `MAX_RETRY_COUNT`).
- **React Components**: Use **PascalCase** for component names (e.g., `UserCard.tsx`).
- **TypeScript Types/Interfaces**: Prefix interfaces with `I` (e.g., `IUser`).
- Avoid abbreviations unless widely understood (e.g., `id` is fine, but avoid `usr` for `user`).

## 4. TypeScript Guidelines
- **Explicit Types**: Always define types for function parameters, return types, and complex objects.
- **Interfaces over Types**: Prefer interfaces for object shapes unless union types or other type-specific features are needed.
- **Avoid `any`**: Use `unknown` or specific types instead of `any` to maintain type safety.
- **Use Generics**: Leverage generics for reusable, type-safe components or utilities.
- **Enums**: Use TypeScript `enum` for fixed sets of values (e.g., `enum UserRole { ADMIN, USER }`).

Example:
```typescript
interface IUser {
id: string;
name: string;
role: UserRole;
}

enum UserRole {
ADMIN = 'admin',
USER = 'user',
}

function fetchUser<T extends IUser>(id: string): Promise<T> {
// Implementation
}
```

## 5. JavaScript/TypeScript Coding Standards
- Indentation: Use 2 spaces for indentation.
 Semicolons: Always use semicolons to terminate statements.
- Quotes: Use single quotes (') for strings unless template literals are required.
- Arrow Functions: Prefer arrow functions for callbacks and concise functions.
- Destructuring: Use destructuring for objects and arrays to improve readability.
- Error Handling: Always use try/catch for async operations and provide meaningful error messages.
- Example:
```typescript
const { id, name } = user;
const fetchData = async (userId: string): Promise<IUser> => {
  try {
    const response = await api.get(`/users/${userId}`);
    return response.data;
  } catch (error) {
    throw new Error(`Failed to fetch user: ${error.message}`);
  }
};
```


## 6. NestJS-Specific Guidelines
- Modular Structure: Group related controllers, services, and modules by feature.
- Dependency Injection: Use NestJS's dependency injection for services and providers.
- DTOs: Use Data Transfer Objects (DTOs) with class-validator for input validation.
- Pipes: Leverage built-in pipes like ValidationPipe for request validation.
- Interceptors: Use interceptors for cross-cutting concerns like logging or response transformation.

```typescript
import { IsString, IsNotEmpty } from 'class-validator';

export class CreateUserDto {
  @IsString()
  @IsNotEmpty()
  name: string;

  @IsString()
  @IsNotEmpty()
  email: string;
}
```


## 7. React-Specific Guidelines
- Functional Components: Use functional components with hooks instead of class components.
- Hooks: Use custom hooks for reusable logic (e.g., useFetchUser).
- State Management: Prefer React Context or lightweight libraries like Zustand for global state.
- Props Typing: Define prop types using interfaces (e.g., interface UserCardProps).
- Tailwind CSS: Use Tailwind CSS for styling, following utility-first principles.
- Avoid Inline Styles: Use Tailwind classes or CSS modules instead of inline styles
