# Design Document: Fantasy Football Demo

## Overview

The Fantasy Football Demo is a single-page web application built with vanilla HTML5, CSS3, and JavaScript. It simulates a fantasy football game experience using mock data and localStorage for persistence. The application follows a component-based architecture with clear separation between UI rendering, state management, and data persistence layers.

The app provides an intuitive mobile-first interface with smooth navigation between sections (Home, League Creation, Team Creation, Team View, Ranking). All data operations are performed client-side with no backend dependencies.

## Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────┐
│           User Interface Layer          │
│  (HTML Templates + CSS Styling)         │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│        Application Logic Layer          │
│  - Navigation Controller                │
│  - League Manager                       │
│  - Team Manager                         │
│  - Player Manager                       │
│  - Ranking Calculator                   │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│         Data Persistence Layer          │
│  (LocalStorage Wrapper)                 │
└─────────────────────────────────────────┘
```

### Technology Stack

- **HTML5**: Semantic markup for structure
- **CSS3**: Modern styling with flexbox/grid, animations, responsive design
- **JavaScript (ES6+)**: Vanilla JavaScript for all logic
- **LocalStorage API**: Client-side data persistence
- **No external dependencies**: Self-contained application

### File Structure

```
/
├── index.html          # Main HTML structure
├── style.css           # All styling and animations
└── script.js           # Application logic and state management
```

## Components and Interfaces

### 1. Navigation Controller

**Responsibility**: Manages view transitions and bottom navigation state

**Interface**:
```javascript
NavigationController {
  navigateTo(viewName: string): void
  updateActiveNavButton(viewName: string): void
  initializeNavigation(): void
}
```

**Key Functions**:
- `navigateTo(viewName)`: Hides all views, shows target view, updates URL hash
- `updateActiveNavButton(viewName)`: Updates active state on navigation buttons
- `initializeNavigation()`: Sets up event listeners for navigation elements

### 2. League Manager

**Responsibility**: Handles league creation and management

**Interface**:
```javascript
LeagueManager {
  createLeague(name: string, teamCount: number): League
  getLeague(): League | null
  generateMockTeams(count: number): Team[]
  saveLeague(league: League): void
  loadLeague(): League | null
}
```

**Key Functions**:
- `createLeague()`: Validates input, creates league object, generates mock teams
- `generateMockTeams()`: Creates AI teams with random names and players
- `saveLeague()`: Persists league to localStorage
- `loadLeague()`: Retrieves league from localStorage

### 3. Team Manager

**Responsibility**: Manages user team creation and player selection

**Interface**:
```javascript
TeamManager {
  createTeam(name: string): Team
  addPlayerToTeam(player: Player): boolean
  removePlayerFromTeam(playerId: string): void
  getRemainingBudget(): number
  isTeamValid(): boolean
  saveTeam(team: Team): void
  loadTeam(): Team | null
  calculateTeamScore(team: Team): number
}
```

**Key Functions**:
- `createTeam()`: Initializes new team with name and starting budget
- `addPlayerToTeam()`: Validates budget/limits, adds player, updates budget
- `removePlayerFromTeam()`: Removes player, refunds budget
- `getRemainingBudget()`: Returns current available budget
- `calculateTeamScore()`: Sums all player points for total score

### 4. Player Manager

**Responsibility**: Generates and manages mock player data

**Interface**:
```javascript
PlayerManager {
  generateMockPlayers(): Player[]
  getPlayersByRole(role: string): Player[]
  getPlayerById(id: string): Player | null
  generateRandomPoints(): number
}
```

**Key Functions**:
- `generateMockPlayers()`: Creates array of mock players with all roles
- `getPlayersByRole()`: Filters players by role for display
- `generateRandomPoints()`: Generates realistic random points (0-10 range)

### 5. Ranking Calculator

**Responsibility**: Calculates and displays team rankings

**Interface**:
```javascript
RankingCalculator {
  calculateRankings(teams: Team[]): RankedTeam[]
  renderRankings(rankings: RankedTeam[]): void
  highlightUserTeam(teamName: string): void
}
```

**Key Functions**:
- `calculateRankings()`: Sorts teams by total score descending
- `renderRankings()`: Generates HTML for ranking display
- `highlightUserTeam()`: Applies visual highlight to user's team

### 6. Storage Manager

**Responsibility**: Abstracts localStorage operations

**Interface**:
```javascript
StorageManager {
  save(key: string, data: any): void
  load(key: string): any | null
  remove(key: string): void
  clear(): void
}
```

**Key Functions**:
- `save()`: Serializes and stores data in localStorage
- `load()`: Retrieves and deserializes data from localStorage
- `remove()`: Deletes specific key from localStorage
- `clear()`: Removes all app data from localStorage

## Data Models

### Player Model

```javascript
Player {
  id: string              // Unique identifier (UUID or incremental)
  name: string            // Mock player name (e.g., "Marco Rossi")
  role: string            // "Goalkeeper" | "Defender" | "Midfielder" | "Attacker"
  value: number           // Player cost (10-100 range)
  points: number          // Current match points (0-10 range)
}
```

**Validation Rules**:
- `id`: Must be unique across all players
- `name`: Non-empty string, 2-30 characters
- `role`: Must be one of four valid roles
- `value`: Integer between 10-100
- `points`: Float between 0-10

### Team Model

```javascript
Team {
  id: string              // Unique identifier
  name: string            // Team name
  players: Player[]       // Array of selected players
  budget: number          // Remaining budget
  totalScore: number      // Sum of all player points
  isUserTeam: boolean     // True if created by user
}
```

**Validation Rules**:
- `name`: Non-empty string, 3-30 characters
- `players`: Array with 0-25 players
- `budget`: Non-negative number
- `totalScore`: Calculated field, always >= 0

### League Model

```javascript
League {
  id: string              // Unique identifier
  name: string            // League name
  teams: Team[]           // All teams in league
  teamCount: number       // Total number of teams
  createdAt: timestamp    // Creation timestamp
}
```

**Validation Rules**:
- `name`: Non-empty string, 3-50 characters
- `teams`: Array with length matching teamCount
- `teamCount`: Integer between 2-20

### RankedTeam Model

```javascript
RankedTeam {
  rank: number            // Position in ranking (1-based)
  team: Team              // Team object
  totalScore: number      // Total points
}
```

## Correctness Properties

*A property is a characteristic or behavior that should hold true across all valid executions of a system—essentially, a formal statement about what the system should do. Properties serve as the bridge between human-readable specifications and machine-verifiable correctness guarantees.*


### Property 1: Navigation displays correct view

*For any* valid view name (home, create-league, create-team, team, ranking), when navigation is triggered to that view, the corresponding section should be visible and all other sections should be hidden.

**Validates: Requirements 1.3**

### Property 2: League creation with valid data persists correctly

*For any* valid league name and team count, creating a league should result in a league object stored in localStorage that can be retrieved with all original data intact.

**Validates: Requirements 2.2, 7.1**

### Property 3: Generated teams match specified count

*For any* valid team count between 2-20, generating mock teams should produce exactly that number of teams.

**Validates: Requirements 2.4**

### Property 4: Players are organized by role

*For any* set of generated players, when grouped by role, all players with the same role should be in the same group and no player should appear in multiple groups.

**Validates: Requirements 3.2**

### Property 5: Budget invariant maintained

*For any* team with selected players, the remaining budget should always equal the initial budget minus the sum of all selected player values.

**Validates: Requirements 3.3, 3.6**

### Property 6: Budget constraint prevents invalid selections

*For any* player whose value exceeds the current remaining budget, attempting to add that player to the team should be rejected and the team state should remain unchanged.

**Validates: Requirements 3.4**

### Property 7: Maximum player limit enforced

*For any* team at maximum capacity, attempting to add another player should be rejected and the team state should remain unchanged.

**Validates: Requirements 3.5**

### Property 8: Team data persistence round-trip

*For any* valid team object, saving it to localStorage and then loading it should produce an equivalent team with all player data intact.

**Validates: Requirements 3.7, 7.2, 7.3**

### Property 9: Player display contains required information

*For any* player rendered in the team view, the rendered HTML should contain the player's name, role, and current points.

**Validates: Requirements 4.3**

### Property 10: Team score calculation correctness

*For any* team with selected players, the calculated total score should equal the sum of all individual player points.

**Validates: Requirements 4.4**

### Property 11: Rankings sorted by score descending

*For any* set of teams with scores, the ranking list should be ordered such that for any two adjacent teams, the team with higher rank has a score greater than or equal to the team with lower rank.

**Validates: Requirements 5.1, 5.4**

### Property 12: User team highlighted in rankings

*For any* ranking list containing the user's team, the user's team should have a visual highlight indicator that distinguishes it from other teams.

**Validates: Requirements 5.2**

### Property 13: Ranking display contains required information

*For any* team in the ranking list, the rendered HTML should contain the team name and total points.

**Validates: Requirements 5.3**

### Property 14: Generated players have unique IDs

*For any* set of generated mock players, all player IDs should be unique with no duplicates.

**Validates: Requirements 6.1**

### Property 15: Minimum players per role

*For any* role (Goalkeeper, Defender, Midfielder, Attacker), the generated player set should contain at least 3 players with that role.

**Validates: Requirements 6.2**

### Property 16: Player values within valid range

*For any* generated player, the value should be an integer between 10 and 100 inclusive.

**Validates: Requirements 6.3**

### Property 17: Player points within valid range

*For any* generated player, the points should be a number between 0 and 10 inclusive.

**Validates: Requirements 6.4**

### Property 18: Corrupted storage handled gracefully

*For any* corrupted or invalid data in localStorage, attempting to load should return null or empty state without throwing errors.

**Validates: Requirements 7.4**

### Property 19: Storage updates are immediate

*For any* data modification operation, the corresponding localStorage entry should be updated synchronously before the operation completes.

**Validates: Requirements 7.5**

## Error Handling

### Input Validation Errors

**Empty League Name**:
- Trigger: User submits league creation form with empty name
- Handling: Display error message "League name is required", prevent form submission
- Recovery: User can correct input and resubmit

**Empty Team Name**:
- Trigger: User submits team creation form with empty name
- Handling: Display error message "Team name is required", prevent form submission
- Recovery: User can correct input and resubmit

**Insufficient Budget**:
- Trigger: User attempts to select player whose value exceeds remaining budget
- Handling: Display error message "Insufficient budget for this player", disable player selection button
- Recovery: User can deselect other players to free up budget

**Maximum Players Reached**:
- Trigger: User attempts to add player when team is at maximum capacity
- Handling: Display error message "Maximum player limit reached", disable all player selection buttons
- Recovery: User can remove players to make room

### Data Persistence Errors

**LocalStorage Not Available**:
- Trigger: Browser doesn't support localStorage or it's disabled
- Handling: Display warning message "Data persistence unavailable, progress will not be saved"
- Recovery: App continues to function with in-memory state only

**LocalStorage Quota Exceeded**:
- Trigger: Attempting to save data when localStorage is full
- Handling: Display error message "Unable to save data, storage full"
- Recovery: User can clear old data or use browser with more storage

**Corrupted Data**:
- Trigger: Loading data from localStorage that is invalid JSON or has wrong structure
- Handling: Log error to console, initialize with empty state
- Recovery: App starts fresh, user can recreate data

### Navigation Errors

**Invalid View Name**:
- Trigger: Attempting to navigate to non-existent view
- Handling: Log warning to console, navigate to home view as fallback
- Recovery: User is redirected to safe default state

## Testing Strategy

### Dual Testing Approach

This application will use both **unit tests** and **property-based tests** to ensure comprehensive coverage:

- **Unit tests**: Verify specific examples, edge cases, and error conditions
- **Property tests**: Verify universal properties across all inputs

Both testing approaches are complementary and necessary. Unit tests catch concrete bugs in specific scenarios, while property tests verify general correctness across a wide range of inputs.

### Property-Based Testing

**Framework**: We will use **fast-check** (JavaScript property-based testing library) for implementing property tests.

**Configuration**:
- Each property test will run a minimum of **100 iterations** to ensure thorough coverage
- Each test will be tagged with a comment referencing the design property:
  - Format: `// Feature: fantasy-football-demo, Property N: [property description]`

**Property Test Coverage**:
Each of the 19 correctness properties defined above will be implemented as a single property-based test. The tests will generate random valid inputs and verify that the specified property holds across all generated cases.

### Unit Testing

**Framework**: We will use **Jest** or browser-native testing for unit tests.

**Unit Test Focus**:
- Specific examples demonstrating correct behavior (e.g., creating a league with name "Serie A" and 10 teams)
- Edge cases (empty teams, zero budget, single player)
- Error conditions (invalid input, storage failures)
- Integration between components (navigation triggering view updates)

**Balance**: We will write focused unit tests for critical paths and edge cases, but avoid excessive unit testing since property-based tests handle broad input coverage.

### Test Organization

```
/tests
├── unit/
│   ├── navigation.test.js
│   ├── league-manager.test.js
│   ├── team-manager.test.js
│   ├── player-manager.test.js
│   ├── ranking-calculator.test.js
│   └── storage-manager.test.js
└── properties/
    ├── navigation.properties.test.js
    ├── league.properties.test.js
    ├── team.properties.test.js
    ├── player.properties.test.js
    ├── ranking.properties.test.js
    └── storage.properties.test.js
```

### Manual Testing

In addition to automated tests, manual testing will verify:
- Visual design and responsiveness across devices
- Animation smoothness and timing
- User experience flow through complete scenarios
- Accessibility with keyboard navigation and screen readers

## Implementation Notes

### Performance Considerations

- **LocalStorage Operations**: Minimize localStorage writes by batching updates
- **Rendering**: Use document fragments for bulk DOM updates to avoid reflows
- **Player Generation**: Generate players once on app initialization, cache in memory

### Browser Compatibility

Target modern browsers with ES6+ support:
- Chrome 60+
- Firefox 60+
- Safari 12+
- Edge 79+

### Accessibility

- Use semantic HTML5 elements (nav, main, section, article)
- Provide ARIA labels for interactive elements
- Ensure keyboard navigation works for all features
- Maintain sufficient color contrast ratios (WCAG AA)

### Future Extensibility

The modular architecture allows for future enhancements:
- Backend integration (replace localStorage with API calls)
- Real-time multiplayer features (WebSocket integration)
- Advanced statistics and analytics
- Player trading between teams
- Multiple leagues per user
- Social features (chat, comments)
