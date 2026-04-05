---
name: write-meta-prompt
description: Expert in transforming vague ideas into professional, structured prompts optimized for Android Engineering. Use this skill when you need to create clear, actionable prompts for AI agents or team members.
version: 1.0.0
usage: "skill: write-meta-prompt [task description]"
---

# Prompt Writer Skill

## Description
Transforms vague, high-level, or unstructured requests into precise, comprehensive, and actionable prompts for specialized AI agents or engineering teams.

## Usage
```bash
skill: prompt-writer [your vague task description]
```

**Example**:
```bash
skill: prompt-writer "I need to fix the login screen, it's slow"
```

## When to Use

Use this skill when you need to:
1. **Clarify Intent**: Transform vague requirements into specific technical goals
2. **Structure Requests**: Organize information into actionable sections
3. **Add Context**: Include necessary Android/Kotlin technical context
4. **Target Audience**: Tailor prompts for specific roles (Dev, SDET, Reviewer)

## Capabilities

### 1. Intent Clarification
- Identifies core technical goals
- Extracts implicit requirements
- Determines scope (File, Module, Project)

### 2. Prompt Structuring
- **Role Definition**: Who should execute the task
- **Context**: Necessary background information
- **Task**: Specific action items
- **Constraints**: What NOT to do
- **Output Format**: Expected deliverable format

### 3. Android-Specific Enhancement
Automatically adds relevant context for:
- **Architecture**: MVI/MVVM, Clean Architecture, Modularization
- **Tech Stack**: Kotlin, Coroutines, Flow, Jetpack Compose, Koin
- **Testing**: JUnit, MockK, Turbine, Paparazzi
- **Performance**: Threading, memory, recomposition

## Reference Files

- [prompt-templates.md](references/prompt-templates.md) - Standard prompt templates
- [android-context.md](references/android-context.md) - Android-specific context patterns
- [examples.md](references/examples.md) - Before/after prompt examples

## Output Format

The skill generates a structured prompt ready to use:

```markdown
# [Role Name] Task

**Objective**: [Clear statement of the goal]

**Context**:
[Relevant background information, current state, dependencies]

**Requirements**:
1. [Requirement 1]
2. [Requirement 2]
...

**Constraints**:
- [Constraint 1]
- [Constraint 2]

**Expected Output**:
[Description of desired artifact]
```

## Example Workflow

**User Input (Vague)**:
```
"I need to fix the login screen, it's slow and the code is a mess. Also add tests."
```

**Skill Output (Structured)**:
```markdown
# Task 1: Senior Android Engineer - Refactor Login Feature

**Objective**: Refactor the Login feature to improve performance and code quality.

**Context**:
- Current implementation: `LoginScreen.kt` and `LoginViewModel.kt`
- Issues: UI lag, poor maintainability
- Architecture: Must follow MVI pattern

**Requirements**:
1. Refactor ViewModel to follow MVI (State, Event, Effect)
2. Extract business logic to `LoginUseCase`
3. Optimize UI composables to reduce recompositions
4. Ensure all operations use appropriate dispatchers

**Constraints**:
- Maintain existing UI design and styling
- No new external libraries without justification
- Preserve existing API contracts

**Expected Output**:
- Refactored Kotlin files following project structure
- Updated DI configuration
- Performance improvements documented

---

# Task 2: Senior SDET - Add Comprehensive Tests

**Objective**: Add test coverage for refactored Login feature.

**Requirements**:
1. Create `LoginViewModelTest` covering all state transitions
2. Create `LoginUseCaseTest` covering success/failure cases
3. Create `LoginScreenSnapshotTest` for all UI states

**Expected Output**:
- Test files in appropriate test directories
- All tests passing with >80% coverage
```

## Best Practices

1. **Be Specific**: Transform "make it better" into "reduce recompositions by 50%"
2. **Add Context**: Include relevant architecture patterns and constraints
3. **Target Audience**: Identify who will execute (Dev, SDET, Reviewer)
4. **Break Down**: Complex tasks should be split into multiple focused prompts
5. **Include Examples**: When possible, provide code examples or patterns to follow

## Common Transformations

| Vague Request | Structured Prompt |
|---------------|-------------------|
| "Fix the bug" | "Fix NullPointerException in UserViewModel.onLogin() caused by..." |
| "Make it faster" | "Optimize GlucoseChart recomposition by using remember/derivedStateOf..." |
| "Add tests" | "Create unit tests for TimeInRangeUseCase covering happy path, errors, edge cases..." |
| "Refactor this" | "Refactor SettingsScreen to follow MVI pattern: extract ViewState, ViewEvent, SideEffect..." |

## Related Skills

- **code-reviewer**: For reviewing generated code
- **unit-test-writer**: For creating test implementations
- **ui-layer**: For scaffolding UI/Presentation layer (features)
- **logic-layer**: For creating Logic layer (components)

---

**Last Updated**: January 2026  
**Project**: CGM OTC Android
