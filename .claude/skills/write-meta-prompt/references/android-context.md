# Android-Specific Context Patterns

This document provides Android-specific context that should be added to prompts based on the task type.

## Architecture Context

### MVI Pattern
When working with presentation layer:
```markdown
**Architecture Context**:
- Pattern: MVI (Model-View-Intent)
- Components:
  - ViewState: Immutable UI state snapshot
  - ViewEvent: User actions/UI events
  - SideEffect: One-off effects (navigation, toasts)
  - ViewModel: State management with unidirectional data flow
```

### Clean Architecture
When working with domain/data layers:
```markdown
**Architecture Context**:
- Layer: [Domain/Data/Presentation]
- Module: `component/[name]` or `feature/[name]`
- Dependencies:
  - Domain: Pure Kotlin, no Android dependencies
  - Data: Repository implementations, data sources
  - Presentation: ViewModels, Composables
```

### Module Dependencies
When working with modules:
```markdown
**Module Context**:
- Current Module: `[module-path]`
- Allowed Dependencies:
  - ✅ common/* modules
  - ✅ component/* modules (sparingly)
  - ❌ feature/* modules (forbidden)
  - ❌ app module (forbidden)
```

---

## Technology Stack Context

### Kotlin Coroutines
When working with async operations:
```markdown
**Coroutines Context**:
- Dispatchers:
  - `named(Dispatcher.IO)`: Network, database operations
  - `named(Dispatcher.DEFAULT)`: CPU-intensive work
  - `named(Dispatcher.MAIN)`: UI updates
- Scope:
  - ViewModels: Use `viewModelScope`
  - Repositories: Inject `CoroutineDispatcher`
- Testing: Use `UnconfinedTestDispatcher` from `BaseTest`
```

### Jetpack Compose
When working with UI:
```markdown
**Compose Context**:
- Design System: Use Jello components only
- State: Use `remember`, `derivedStateOf` for performance
- Side Effects: Use `LaunchedEffect` for one-time effects
- Recomposition: Optimize with stable parameters
- Theme: Always wrap in `JelloAccuchekTheme`
```

### Dependency Injection (Koin)
When working with DI:
```markdown
**DI Context**:
- Framework: Koin
- Configuration: `app/di/[Module]Module.kt`
- Scopes:
  - `single`: Repositories, Handlers, Managers
  - `factory`: UseCases
  - `viewModel`: ViewModels
- Qualifiers: Use `named(Dispatcher.IO)`, `named(Dispatcher.DEFAULT)` for dispatchers
```

### Navigation
When working with navigation:
```markdown
**Navigation Context**:
- Location: All navigation in `app/navigation/`
- Type-Safe: Kotlin Serialization routes
- Pattern:
  - Features expose screens only
  - Navigation handled at app level
  - Side effects for navigation decisions
```

---

## Testing Context

### Unit Testing
When requesting unit tests:
```markdown
**Testing Context**:
- Framework: JUnit + MockK
- Base Class: Extend `BaseTest()` for coroutines/dispatchers
- Naming: Use GIVEN/WHEN/THEN format
- Coverage: Target >80% for UseCases, >75% for ViewModels
- Structure:
  - `@Before override fun setup()`: Initialize SUT
  - `@Test`: Test methods with descriptive names
```

### Snapshot Testing
When requesting UI tests:
```markdown
**Snapshot Testing Context**:
- Framework: Paparazzi
- Rule: `PaparazziTestRule()` with `SnapshotConfig`
- Theme: Wrap in `JelloAccuchekTheme`
- States: Test Loading, Success, Error, Empty
- Parameters: Use `TestParameterInjector` for multiple states
```

---

## Performance Context

### UI Performance
When optimizing UI:
```markdown
**Performance Context**:
- Recomposition: Minimize using `remember`, `derivedStateOf`
- Stable Parameters: Use immutable data classes
- Heavy Operations: Move to background thread
- LazyColumn: Use `key` parameter for stable items
```

### Threading
When working with background tasks:
```markdown
**Threading Context**:
- Main Thread: UI updates only
- IO Dispatcher: Network, database, file operations
- Default Dispatcher: CPU-intensive calculations
- Testing: `UnconfinedTestDispatcher` for tests
```

### Memory
When optimizing memory:
```markdown
**Memory Context**:
- Lifecycle: Use `viewModelScope`, avoid `GlobalScope`
- Cleanup: Implement `onDispose` in composables
- Leaks: Avoid storing Activity/Context references
```

---

## Quality Standards Context

### Code Documentation
Always include:
```markdown
**Documentation Requirements**:
- KDoc: Mandatory for all public APIs
- Format:
  - Description of what the component does
  - @param for each parameter
  - @return for return values
  - Side effects section
```

### Error Handling
Always include:
```markdown
**Error Handling Requirements**:
- Use `Result<T>` for expected failures
- Use exceptions for programmer errors only
- Provide meaningful error messages
- Handle all error cases in UI
```

### Code Style
Always include:
```markdown
**Code Style Requirements**:
- Follow Kotlin coding conventions
- Use meaningful variable names
- Keep functions small and focused
- Avoid hardcoded values (strings, colors, dimensions)
- Use project's design system (Jello)
```

---

## Context Selection Guide

### By Task Type

| Task Type | Include Context |
|-----------|-----------------|
| New Feature | MVI, Clean Architecture, Compose, DI, Navigation |
| New Component | Clean Architecture, Coroutines, DI |
| UI Work | Compose, Jello Design System, Performance |
| Testing | Unit/Snapshot Testing, Coverage targets |
| Bug Fix | Relevant tech stack, Error Handling |
| Refactoring | Architecture, Code Style, Performance |

### By Module Type

| Module | Include Context |
|--------|-----------------|
| `feature/*` | MVI, Compose, Navigation, DI |
| `component/*/domain` | Clean Architecture, Coroutines |
| `component/*/data` | Clean Architecture, DI, Threading |
| `common/*` | Kotlin best practices, No Android deps |
| `app` | DI, Navigation, Entry point |

### By Role

| Role | Include Context |
|------|-----------------|
| Android Engineer | Full stack: MVI, Clean Arch, Compose, DI |
| SDET | Testing frameworks, Coverage, Standards |
| Code Reviewer | Quality standards, Architecture patterns |
| Build Engineer | Gradle, Dependencies, Build optimization |

---

## Example Context Additions

### Before (Generic)
```markdown
**Task**: Create a new use case for fetching user data
```

### After (Android-Specific)
```markdown
**Task**: Create a new use case for fetching user data

**Architecture Context**:
- Layer: Domain
- Module: `component/user/domain/usecase/`
- Pattern: Single responsibility, pure business logic
- Dependencies: Repository interface only

**Technical Context**:
- Use `suspend` for async operations
- Inject `Dispatcher.IO` using `named(Dispatcher.IO)`
- Return `Result<User>` for error handling
- Follow constructor injection pattern

**Testing Requirements**:
- Create `GetUserDataUseCaseTest` extending `BaseTest()`
- Test happy path, error cases, edge cases
- Use MockK for repository mock
- Target >80% coverage
```

---

## Quick Reference

### Essential Context Checklist

- [ ] Architecture pattern (MVI/Clean Architecture)
- [ ] Module location and dependencies
- [ ] Tech stack (Kotlin/Coroutines/Compose)
- [ ] Testing requirements
- [ ] Code quality standards
- [ ] Performance considerations

### Context Verbosity Levels

**Minimal** (for experienced devs):
```markdown
Architecture: MVI, Clean Arch
Tech: Kotlin, Coroutines, Compose
Testing: Unit + Snapshot, BaseTest
```

**Standard** (recommended):
```markdown
Include architecture, tech stack, testing, and quality standards
```

**Detailed** (for complex tasks):
```markdown
Include all context sections plus examples and code snippets
```

---

**Last Updated**: January 2026  
**Project**: CGM OTC Android
