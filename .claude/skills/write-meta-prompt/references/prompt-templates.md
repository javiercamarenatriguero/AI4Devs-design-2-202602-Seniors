# Prompt Templates

This document provides standard templates for different types of prompts.

## Template 1: Development Task

Use this template when requesting implementation work.

```markdown
# [Role]: [Task Type] - [Feature/Component Name]

**Objective**: [One-line clear goal]

**Context**:
- Current State: [What exists now]
- Problem: [What needs fixing/improving]
- Architecture: [Relevant patterns - MVI, Clean Architecture, etc.]
- Dependencies: [Required modules, libraries]

**Requirements**:
1. [Functional requirement 1]
2. [Functional requirement 2]
3. [Technical requirement 1]
4. [Technical requirement 2]

**Constraints**:
- [What not to change]
- [What not to use]
- [Performance/size limits]

**Expected Output**:
- [File 1]: [Description]
- [File 2]: [Description]
- [Documentation/Tests requirements]

**Acceptance Criteria**:
- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] All tests pass
- [ ] Lint and detekt checks pass
```

---

## Template 2: Testing Task

Use this template when requesting test creation.

```markdown
# SDET Task: Write Tests for [Component/Feature]

**Objective**: Create comprehensive test coverage for [component/feature name]

**Context**:
- Component: `[path/to/file]`
- Type: [ViewModel/UseCase/Repository/UI]
- Current Coverage: [X%]
- Target Coverage: [Y%]

**Test Requirements**:

### Unit Tests
- [ ] Happy path scenarios
- [ ] Error handling
- [ ] Edge cases
- [ ] Boundary conditions

### Snapshot Tests (if UI)
- [ ] Default state
- [ ] Loading state
- [ ] Error state
- [ ] Success state with data
- [ ] Empty state

**Test Data**:
[Provide sample test data or reference existing test fixtures]

**Expected Output**:
- `[ComponentName]Test.kt` in `src/test/.../`
- `[ComponentName]SnapshotTest.kt` in `src/test/.../` (if UI)
- All tests using GIVEN/WHEN/THEN naming
- All tests extending `BaseTest()` where appropriate

**Acceptance Criteria**:
- [ ] All tests pass
- [ ] Coverage meets target
- [ ] Tests follow project standards
```

---

## Template 3: Refactoring Task

Use this template when requesting code refactoring.

```markdown
# Senior Android Engineer: Refactor [Component/Feature]

**Objective**: Refactor [component] to [improve X/follow Y pattern/fix Z issue]

**Context**:
- Current File(s): `[path/to/files]`
- Current Issues:
  - [Issue 1: e.g., Poor performance]
  - [Issue 2: e.g., Violates architecture]
  - [Issue 3: e.g., Hard to test]
- Target Pattern: [MVI/Clean Architecture/DI/etc.]

**Refactoring Requirements**:
1. **Structure**:
   - [Extract X into Y]
   - [Move Z to W layer]
   
2. **Performance**:
   - [Optimize A]
   - [Reduce B allocations]
   
3. **Architecture**:
   - [Follow MVI pattern]
   - [Separate concerns]

**Constraints**:
- Maintain existing public API
- Preserve existing behavior
- No breaking changes for consumers
- Maintain test coverage

**Expected Output**:
- Refactored files maintaining functionality
- Updated tests (if needed)
- Migration guide (if API changes)

**Acceptance Criteria**:
- [ ] All existing tests still pass
- [ ] New tests added for new structure
- [ ] Performance improved by [X%]
- [ ] Follows architecture guidelines
```

---

## Template 4: Bug Fix Task

Use this template when requesting bug fixes.

```markdown
# Android Engineer: Fix Bug - [Bug Title]

**Objective**: Fix [specific bug description]

**Bug Details**:
- **Ticket**: [OTCT-XXX]
- **Severity**: [Critical/High/Medium/Low]
- **Affected Component**: `[file/module]`
- **Affected Versions**: [version range]

**Current Behavior**:
[Describe what currently happens - steps to reproduce]

**Expected Behavior**:
[Describe what should happen]

**Root Cause Analysis** (if known):
[Explanation of why the bug occurs]

**Fix Requirements**:
1. [Fix specific issue X]
2. [Add validation for Y]
3. [Add test to prevent regression]

**Testing**:
- [ ] Unit test added to reproduce bug
- [ ] Unit test verifies fix
- [ ] Manual testing performed
- [ ] Edge cases covered

**Expected Output**:
- Fixed code in `[file path]`
- Regression test in `[test file path]`
- Verification steps documented

**Acceptance Criteria**:
- [ ] Bug no longer reproducible
- [ ] Regression test added
- [ ] All tests pass
- [ ] No side effects introduced
```

---

## Template 5: Code Review Task

Use this template when requesting code review.

```markdown
# Code Reviewer: Review [Feature/PR]

**Objective**: Review [feature/PR] for quality, architecture, and best practices

**Review Scope**:
- **Files Changed**: [Number of files]
- **Lines Changed**: [+XXX/-YYY]
- **Type**: [Feature/Bug Fix/Refactor]

**Review Focus Areas**:

### Architecture
- [ ] Follows MVI pattern
- [ ] Proper layer separation
- [ ] Correct module dependencies

### Code Quality
- [ ] KDoc present for public APIs
- [ ] No code smells
- [ ] Proper error handling
- [ ] Thread safety

### Testing
- [ ] Unit tests added
- [ ] Snapshot tests added (if UI)
- [ ] Tests follow GIVEN/WHEN/THEN
- [ ] Edge cases covered

### Performance
- [ ] No main thread blocking
- [ ] Proper dispatcher usage
- [ ] No memory leaks

**Expected Output**:
Review comments using Conventional Comments format:
- `suggestion:` for improvements
- `issue:` for must-fix problems
- `question:` for clarifications
- `praise:` for good work

**Review Outcome**:
- [ ] Approve
- [ ] Approve with minor suggestions
- [ ] Request changes
```

---

## Template 6: Feature Scaffolding Task

Use this template when creating new features from scratch.

```markdown
# Android Engineer: Scaffold [Feature Name] Feature

**Objective**: Create complete feature module for [feature name]

**Feature Description**:
[Brief description of what the feature does]

**Architecture Components**:

### Domain Layer
- [ ] `[Feature]ViewState` - UI state model
- [ ] `[Feature]ViewEvent` - User actions
- [ ] `[Feature]SideEffect` - One-off effects
- [ ] `[Feature]UseCase` (if needed)

### Presentation Layer
- [ ] `[Feature]ViewModel` - MVI implementation
- [ ] `[Feature]Screen` - Composable UI
- [ ] `[Feature]Contract` - Contract definition

### Navigation
- [ ] `[Feature]Route` - Navigation route
- [ ] `[Feature]Navigation.kt` - Navigation wiring

### DI
- [ ] Register ViewModel in `ViewModelModule.kt`
- [ ] Register dependencies (if any)

**UI Requirements**:
- [List key UI elements]
- [List user interactions]
- [List states to handle]

**Expected Output**:
- Complete feature module following project structure
- All files properly documented with KDoc
- Navigation integrated
- Basic tests included

**Acceptance Criteria**:
- [ ] Feature compiles without errors
- [ ] Feature navigable from other screens
- [ ] Follows MVI pattern
- [ ] Basic tests pass
```

---

## Usage Guidelines

### Choosing the Right Template

| Task Type | Use Template |
|-----------|--------------|
| Implementing new feature | Template 1 or 6 |
| Writing tests | Template 2 |
| Improving existing code | Template 3 |
| Fixing a bug | Template 4 |
| Reviewing code | Template 5 |

### Customizing Templates

1. Replace `[placeholders]` with specific values
2. Add project-specific context
3. Include relevant file paths
4. Reference architecture docs when needed
5. Add examples where helpful

### Template Best Practices

- **Be Specific**: Replace generic terms with actual names
- **Add Context**: Include relevant background information
- **Set Clear Expectations**: Define what "done" looks like
- **Include Examples**: Show code patterns when possible
- **Reference Standards**: Link to architecture/style guides

---

**Last Updated**: January 2026  
**Project**: CGM OTC Android
