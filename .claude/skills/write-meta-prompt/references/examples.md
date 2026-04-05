# Prompt Examples: Before and After

This document shows real-world examples of transforming vague prompts into structured, actionable prompts.

## Example 1: Feature Request

### ❌ Before (Vague)
```
"I need a new screen for user settings"
```

### ✅ After (Structured)
```markdown
# Android Engineer: Create User Settings Feature

**Objective**: Implement a new Settings screen for user preferences

**Context**:
- Module: `feature/user-settings`
- Architecture: MVI pattern, Clean Architecture
- Navigation: Accessible from bottom navigation bar
- Existing: User authentication already implemented

**Requirements**:

### Domain Layer
1. Create `UserSettingsViewState` with:
   - `notificationsEnabled: Boolean`
   - `glucoseUnit: GlucoseUnit`
   - `language: String`
   
2. Create `UserSettingsViewEvent` for:
   - Toggle notifications
   - Change glucose unit
   - Change language
   
3. Create `UserSettingsSideEffect` for:
   - Navigation back
   - Show confirmation toasts

### Presentation Layer
4. Create `UserSettingsViewModel` following MVI pattern
5. Create `UserSettingsScreen` using Jello components
6. Register ViewModel in DI

### Navigation
7. Add route in `app/navigation/settings/`
8. Wire to bottom navigation

**Constraints**:
- Must use Jello design system components
- Settings must persist across app restarts
- No hardcoded strings (use string resources)

**Expected Output**:
- `feature/user-settings/` module with complete implementation
- Unit tests for ViewModel (>75% coverage)
- Snapshot tests for all UI states
- DI configuration updated
- Navigation wired

**Acceptance Criteria**:
- [ ] All settings are functional
- [ ] Settings persist correctly
- [ ] UI follows design system
- [ ] All tests pass
- [ ] Navigation works correctly
```

---

## Example 2: Bug Fix

### ❌ Before (Vague)
```
"The app crashes sometimes when loading glucose data"
```

### ✅ After (Structured)
```markdown
# Android Engineer: Fix Crash in Glucose Data Loading

**Objective**: Fix NullPointerException in glucose data loading

**Bug Details**:
- **Ticket**: OTCT-XXX
- **Severity**: High
- **Affected Component**: `component/cgm/data/repository/GlucoseRepositoryImpl.kt`
- **Error**: `NullPointerException` at line 45
- **Frequency**: Intermittent (~20% of data loads)

**Current Behavior**:
1. User opens Today screen
2. App attempts to load glucose measurements
3. Crash occurs if sensor is disconnected during load
4. Stack trace shows NPE in `GlucoseRepositoryImpl.mapToGlucoseData()`

**Expected Behavior**:
1. User opens Today screen
2. App loads glucose measurements
3. If sensor disconnected, show "No data available" message
4. No crash occurs

**Root Cause**:
The `sensorData` field can be null when sensor is disconnected, but code doesn't check before accessing `.measurements` property.

**Fix Requirements**:
1. Add null-check for `sensorData` before accessing properties
2. Return `Result.failure()` with appropriate error when data is null
3. Update UI to handle "sensor disconnected" error state
4. Add unit test to reproduce and verify fix

**Expected Output**:
```kotlin
// In GlucoseRepositoryImpl.kt
override suspend fun getGlucoseData(): Result<List<GlucoseData>> {
    return withContext(ioDispatcher) {
        val sensorData = dataStore.getSensorData()
        
        if (sensorData == null) {
            return@withContext Result.failure(
                SensorDisconnectedException("Sensor not connected")
            )
        }
        
        // Safe to access measurements now
        Result.success(sensorData.measurements.map { it.toGlucoseData() })
    }
}

// In GlucoseRepositoryImplTest.kt
@Test
fun `SHOULD return failure WHEN getSensorData is null`() = runTest {
    // Test implementation
}
```

**Acceptance Criteria**:
- [ ] Crash no longer reproducible
- [ ] UI shows appropriate error message
- [ ] Regression test added and passing
- [ ] All existing tests still pass
```

---

## Example 3: Performance Optimization

### ❌ Before (Vague)
```
"The glucose chart is slow and laggy"
```

### ✅ After (Structured)
```markdown
# Android Engineer: Optimize Glucose Chart Performance

**Objective**: Reduce recompositions and improve rendering performance of GlucoseChart

**Context**:
- Component: `feature/today/ui/components/GlucoseChart.kt`
- Current Performance: ~500ms render time, 20+ recompositions per second
- Target Performance: <100ms render time, <5 recompositions per second
- Issue: Chart updates on every state change, even unrelated ones

**Performance Analysis**:
- Chart recomposes on every `TodayViewState` update
- Data processing happens during composition (should be in ViewModel)
- No use of `remember` or `derivedStateOf`
- Creating new objects in composable on every recomposition

**Optimization Requirements**:

### 1. State Optimization
- Extract chart-specific state to dedicated data class
- Use `derivedStateOf` for computed chart points
- Move data processing to ViewModel

### 2. Composition Optimization
- Use `remember` for chart configuration
- Make parameters stable (immutable data classes)
- Extract sub-composables with stable parameters

### 3. Data Processing
- Move chart data calculation to ViewModel
- Pre-process data in background (IO dispatcher)
- Cache processed data points

**Implementation**:

```kotlin
// In TodayViewModel
private val chartData: StateFlow<ChartData> = 
    glucoseMeasurements
        .map { measurements -> processChartData(measurements) }
        .stateIn(viewModelScope, SharingStarted.Lazily, ChartData.Empty)

private fun processChartData(measurements: List<Measurement>): ChartData {
    // Heavy processing here, on background thread
}

// In GlucoseChart
@Composable
fun GlucoseChart(
    chartData: ChartData, // Stable, processed data
    modifier: Modifier = Modifier,
) {
    val chartConfig = remember {
        ChartConfiguration(/* ... */)
    }
    
    // Chart rendering with optimized state
}
```

**Constraints**:
- Must maintain existing visual design
- Chart data must remain accurate
- No breaking changes to chart API

**Expected Output**:
- Refactored `GlucoseChart.kt` with optimizations
- Updated `TodayViewModel.kt` with data processing
- Performance test showing improvements
- Updated unit tests

**Acceptance Criteria**:
- [ ] Render time <100ms (measured with Compose profiler)
- [ ] Recompositions <5 per second during updates
- [ ] All existing tests pass
- [ ] Visual design unchanged
- [ ] Chart remains accurate
```

---

## Example 4: Refactoring

### ❌ Before (Vague)
```
"Clean up the Settings code, it's messy"
```

### ✅ After (Structured)
```markdown
# Senior Android Engineer: Refactor Settings Feature to MVI Pattern

**Objective**: Refactor Settings feature from MVVM to MVI pattern for better state management

**Context**:
- Current Files:
  - `feature/settings/SettingsViewModel.kt` (~300 lines)
  - `feature/settings/SettingsScreen.kt` (~400 lines)
- Current Issues:
  - Multiple LiveData streams (hard to test)
  - Scattered state management
  - Direct navigation from ViewModel
  - Large composables (hard to maintain)
- Target: MVI pattern following project standards

**Refactoring Steps**:

### 1. Create Contract (NEW)
Create `feature/settings/SettingsContract.kt`:
```kotlin
interface SettingsContract {
    data class SettingsViewState(
        val userName: String = "",
        val notificationsEnabled: Boolean = false,
        val glucoseUnit: GlucoseUnit = GlucoseUnit.MG_DL,
        val isLoading: Boolean = false,
    ) : ViewState
    
    sealed interface SettingsViewEvent : ViewEvent {
        data object OnLogoutClicked : SettingsViewEvent
        data object OnAccountClicked : SettingsViewEvent
        data class OnNotificationToggled(val enabled: Boolean) : SettingsViewEvent
    }
    
    sealed interface SettingsSideEffect : SideEffect {
        sealed interface Navigation : SettingsSideEffect {
            data object NavigateToAccount : Navigation
            data object NavigateToLogin : Navigation
        }
        data class ShowToast(val message: String) : SettingsSideEffect
    }
}
```

### 2. Refactor ViewModel
- Implement MVI delegate: `MVI<ViewState, ViewEvent, SideEffect>`
- Convert LiveData to StateFlow
- Move navigation to SideEffects
- Extract business logic to UseCases (if needed)

### 3. Refactor Screen
- Extract large composables to smaller ones:
  - `SettingsHeader()`
  - `SettingsSection()`
  - `SettingsItem()`
- Use composition over large conditional blocks
- Hoist state properly

### 4. Update Navigation
- Handle side effects in navigation layer
- Remove NavController from ViewModel

**Constraints**:
- Maintain existing functionality
- No UI design changes
- All existing tests must pass (after updates)
- Preserve public API for navigation

**Expected Output**:
- `SettingsContract.kt` with ViewState/Event/Effect
- Refactored `SettingsViewModel.kt` using MVI
- Refactored `SettingsScreen.kt` with smaller composables
- Updated navigation in `app/navigation/settings/`
- Updated unit tests for new structure
- Migration tested manually

**Acceptance Criteria**:
- [ ] Follows MVI pattern completely
- [ ] All functionality preserved
- [ ] Tests updated and passing
- [ ] Code more maintainable (smaller files)
- [ ] No breaking changes for callers
```

---

## Example 5: Testing

### ❌ Before (Vague)
```
"Add tests for the TimeInRange component"
```

### ✅ After (Structured)
```markdown
# SDET: Write Comprehensive Tests for TimeInRange Component

**Objective**: Create complete test coverage for TimeInRange component

**Context**:
- Component: `component/timeinrange/`
- Type: Domain & Data layer component
- Current Coverage: 0%
- Target Coverage: >80%

**Component Structure**:
```
component/timeinrange/
├── domain/
│   ├── model/
│   │   ├── TimeInRangeData.kt
│   │   └── GlucoseRange.kt
│   ├── repository/
│   │   └── TimeInRangeRepository.kt
│   └── usecase/
│       ├── GetTimeInRangeUseCase.kt
│       └── GetLast24HoursTimeInRangeUseCase.kt
└── data/
    ├── datasource/
    │   └── GlucoseMeasurementDataSource.kt
    └── repository/
        └── TimeInRangeRepositoryImpl.kt
```

**Test Requirements**:

### 1. Domain Model Tests
File: `GlucoseRangeTest.kt`
- [ ] Test BELOW_RANGE boundary (<70)
- [ ] Test IN_RANGE boundaries (70-180)
- [ ] Test ABOVE_RANGE boundary (>=180)
- [ ] Test edge cases (0, negative, very large values)

File: `TimeInRangeDataTest.kt`
- [ ] Test validation (percentages 0-100)
- [ ] Test calculation correctness
- [ ] Test edge cases (zero measurements, all in range, etc.)

### 2. Use Case Tests
File: `GetTimeInRangeUseCaseTest.kt` extending `BaseTest()`
- [ ] GIVEN repository has data WHEN invoked THEN returns TimeInRangeData
- [ ] GIVEN repository fails WHEN invoked THEN returns failure
- [ ] GIVEN invalid time range WHEN invoked THEN throws exception
- [ ] Verify correct dispatcher usage

File: `GetLast24HoursTimeInRangeUseCaseTest.kt` extending `BaseTest()`
- [ ] GIVEN repository has data WHEN invoked THEN returns 24h data
- [ ] GIVEN no data WHEN invoked THEN returns empty data
- [ ] GIVEN repository fails WHEN invoked THEN returns failure

### 3. Repository Tests
File: `TimeInRangeRepositoryImplTest.kt` extending `BaseTest()`
- [ ] Test correct TIR calculation with mixed data
- [ ] Test with all measurements in range (100%)
- [ ] Test with no measurements (0%)
- [ ] Test boundary values (70.0, 180.0)
- [ ] Test Flow emissions (observeTimeInRange)
- [ ] Test data source error handling

**Test Data**:
```kotlin
// Use these test fixtures
val testMeasurementsBelowRange = listOf(
    GlucoseMeasurement(50.0, timestamp1),
    GlucoseMeasurement(65.0, timestamp2),
)

val testMeasurementsInRange = listOf(
    GlucoseMeasurement(120.0, timestamp1),
    GlucoseMeasurement(150.0, timestamp2),
)

val testMeasurementsAboveRange = listOf(
    GlucoseMeasurement(200.0, timestamp1),
    GlucoseMeasurement(250.0, timestamp2),
)
```

**Test Standards**:
- Use GIVEN/WHEN/THEN naming convention
- Extend `BaseTest()` for coroutines
- Use MockK for mocking
- Use Turbine for Flow testing
- Follow project test structure

**Expected Output**:
- All test files in `src/test/` directory
- 36 total test cases minimum
- All tests passing
- Coverage >80%

**Acceptance Criteria**:
- [ ] All tests pass
- [ ] Coverage target met
- [ ] Tests follow naming convention
- [ ] No flaky tests
- [ ] Tests are maintainable
```

---

## Pattern Recognition Guide

### Identify Task Type

| User Says | Task Type | Use Template |
|-----------|-----------|--------------|
| "Create/Add new..." | Feature/Component | Development Task |
| "Fix/Bug/Crash..." | Bug Fix | Bug Fix Task |
| "Test/Add tests..." | Testing | Testing Task |
| "Optimize/Speed up..." | Performance | Performance Task |
| "Refactor/Clean up..." | Refactoring | Refactoring Task |
| "Review..." | Code Review | Review Task |

### Extract Key Information

Look for:
1. **What**: Component/feature name
2. **Where**: Module/file path
3. **Why**: Problem or goal
4. **How**: Architecture/pattern to use
5. **Who**: Target role (Dev/SDET/Reviewer)

### Add Missing Context

If not specified, infer:
- Architecture pattern from module type
- Tech stack from component type
- Testing requirements from task type
- Performance targets from use case

---

**Last Updated**: January 2026  
**Project**: CGM OTC Android
