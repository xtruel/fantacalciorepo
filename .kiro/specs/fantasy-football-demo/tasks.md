# Implementation Plan: Fantasy Football Demo

## Overview

This implementation plan breaks down the Fantasy Football Demo application into discrete, incremental coding tasks. Each task builds on previous work, with testing integrated throughout to validate functionality early. The implementation follows a bottom-up approach: core data structures and utilities first, then business logic, then UI integration.

## Tasks

- [x] 1. Set up project structure and core data models
  - Create `index.html`, `style.css`, and `script.js` files
  - Define JavaScript data model interfaces (Player, Team, League, RankedTeam) as JSDoc comments
  - Set up basic HTML structure with semantic elements (nav, main, section)
  - _Requirements: 9.1, 9.3_

- [-] 2. Implement Storage Manager
  - [x] 2.1 Create StorageManager module with save, load, remove, and clear methods
    - Implement JSON serialization/deserialization
    - Add error handling for corrupted data
    - _Requirements: 7.1, 7.2, 7.4_

  - [ ] 2.2 Write property test for storage round-trip
    - **Property 8: Team data persistence round-trip**
    - **Validates: Requirements 3.7, 7.2, 7.3**

  - [ ] 2.3 Write property test for corrupted data handling
    - **Property 18: Corrupted storage handled gracefully**
    - **Validates: Requirements 7.4**

  - [ ] 2.4 Write unit tests for StorageManager edge cases
    - Test empty keys, null values, localStorage unavailable
    - _Requirements: 7.4_

- [-] 3. Implement Player Manager and mock data generation
  - [x] 3.1 Create PlayerManager module with generateMockPlayers function
    - Generate at least 3 players per role (Goalkeeper, Defender, Midfielder, Attacker)
    - Assign unique IDs, invented names, values (10-100), and random points (0-10)
    - _Requirements: 6.1, 6.2, 6.3, 6.4_

  - [x] 3.2 Implement getPlayersByRole and getPlayerById helper functions
    - _Requirements: 3.2_

  - [ ] 3.3 Write property test for unique player IDs
    - **Property 14: Generated players have unique IDs**
    - **Validates: Requirements 6.1**

  - [ ] 3.4 Write property test for minimum players per role
    - **Property 15: Minimum players per role**
    - **Validates: Requirements 6.2**

  - [ ] 3.5 Write property test for player value ranges
    - **Property 16: Player values within valid range**
    - **Validates: Requirements 6.3**

  - [ ] 3.6 Write property test for player points ranges
    - **Property 17: Player points within valid range**
    - **Validates: Requirements 6.4**

  - [ ] 3.7 Write property test for players organized by role
    - **Property 4: Players are organized by role**
    - **Validates: Requirements 3.2**

- [ ] 4. Checkpoint - Verify data layer
  - Ensure all tests pass, ask the user if questions arise.

- [-] 5. Implement Team Manager
  - [x] 5.1 Create TeamManager module with createTeam, addPlayerToTeam, removePlayerFromTeam functions
    - Initialize team with starting budget (e.g., 500)
    - Implement budget validation before adding players
    - Enforce maximum player limit (e.g., 25 players)
    - _Requirements: 3.3, 3.4, 3.5_

  - [x] 5.2 Implement getRemainingBudget and calculateTeamScore functions
    - Calculate remaining budget as initial minus sum of player values
    - Calculate team score as sum of all player points
    - _Requirements: 3.6, 4.4_

  - [x] 5.3 Implement saveTeam and loadTeam functions using StorageManager
    - _Requirements: 3.7, 7.2_

  - [ ] 5.4 Write property test for budget invariant
    - **Property 5: Budget invariant maintained**
    - **Validates: Requirements 3.3, 3.6**

  - [ ] 5.5 Write property test for budget constraint enforcement
    - **Property 6: Budget constraint prevents invalid selections**
    - **Validates: Requirements 3.4**

  - [ ] 5.6 Write property test for maximum player limit
    - **Property 7: Maximum player limit enforced**
    - **Validates: Requirements 3.5**

  - [ ] 5.7 Write property test for team score calculation
    - **Property 10: Team score calculation correctness**
    - **Validates: Requirements 4.4**

  - [ ] 5.8 Write unit tests for team creation edge cases
    - Test empty team, single player, full team
    - _Requirements: 3.3, 3.4, 3.5_

- [-] 6. Implement League Manager
  - [x] 6.1 Create LeagueManager module with createLeague and generateMockTeams functions
    - Validate league name is non-empty
    - Generate specified number of mock teams with random names and players
    - _Requirements: 2.2, 2.3, 2.4_

  - [x] 6.2 Implement saveLeague and loadLeague functions using StorageManager
    - _Requirements: 2.2, 7.1_

  - [ ] 6.3 Write property test for league persistence
    - **Property 2: League creation with valid data persists correctly**
    - **Validates: Requirements 2.2, 7.1**

  - [ ] 6.4 Write property test for generated team count
    - **Property 3: Generated teams match specified count**
    - **Validates: Requirements 2.4**

  - [ ] 6.5 Write unit tests for league creation validation
    - Test empty league name rejection
    - _Requirements: 2.3_

- [-] 7. Implement Ranking Calculator
  - [x] 7.1 Create RankingCalculator module with calculateRankings function
    - Sort teams by total score in descending order
    - Assign rank positions (1-based)
    - _Requirements: 5.1, 5.4_

  - [x] 7.2 Implement renderRankings and highlightUserTeam functions
    - Generate HTML for ranking display
    - Apply highlight class to user's team
    - _Requirements: 5.2, 5.3_

  - [ ] 7.3 Write property test for ranking sort order
    - **Property 11: Rankings sorted by score descending**
    - **Validates: Requirements 5.1, 5.4**

  - [ ] 7.4 Write property test for user team highlighting
    - **Property 12: User team highlighted in rankings**
    - **Validates: Requirements 5.2**

  - [ ] 7.5 Write property test for ranking display information
    - **Property 13: Ranking display contains required information**
    - **Validates: Requirements 5.3**

  - [ ] 7.6 Write unit tests for ranking edge cases
    - Test empty team list, single team, tied scores
    - _Requirements: 5.5_

- [ ] 8. Checkpoint - Verify business logic layer
  - Ensure all tests pass, ask the user if questions arise.

- [-] 9. Implement Navigation Controller
  - [x] 9.1 Create NavigationController module with navigateTo and updateActiveNavButton functions
    - Hide all view sections, show target view
    - Update active state on navigation buttons
    - Update URL hash for browser history
    - _Requirements: 1.3_

  - [x] 9.2 Implement initializeNavigation function to set up event listeners
    - Attach click handlers to all navigation elements
    - Handle initial page load and hash changes
    - _Requirements: 1.2, 1.3_

  - [ ] 9.3 Write property test for navigation view switching
    - **Property 1: Navigation displays correct view**
    - **Validates: Requirements 1.3**

  - [ ] 9.4 Write unit tests for navigation edge cases
    - Test invalid view names, initial load, back button
    - _Requirements: 1.3_

- [ ] 10. Build HTML structure for all views
  - [ ] 10.1 Create home view HTML
    - Add logo placeholder, title, navigation buttons
    - Add bottom navigation bar
    - _Requirements: 1.1, 1.2_

  - [ ] 10.2 Create league creation view HTML
    - Add form with league name input and team count selector
    - Add submit button and error message container
    - _Requirements: 2.1_

  - [ ] 10.3 Create team creation view HTML
    - Add form with team name input and budget display
    - Add player list container with role sections
    - Add player selection checkboxes/buttons
    - _Requirements: 3.1_

  - [ ] 10.4 Create team view HTML
    - Add stylized football field container
    - Add player position containers for each role
    - Add total score display
    - _Requirements: 4.1_

  - [ ] 10.5 Create ranking view HTML
    - Add ranking list container
    - Add empty state message container
    - _Requirements: 5.1_

- [ ] 11. Implement CSS styling
  - [ ] 11.1 Create base styles and CSS variables
    - Define color scheme (blue, green, orange)
    - Set up typography and spacing system
    - _Requirements: 8.3_

  - [ ] 11.2 Style navigation and layout
    - Style bottom navigation bar with icons
    - Create responsive grid/flexbox layouts
    - _Requirements: 1.2, 8.2_

  - [ ] 11.3 Style cards and form elements
    - Apply rounded corners to all cards
    - Style input fields, buttons, checkboxes
    - _Requirements: 8.2_

  - [ ] 11.4 Style football field and player positions
    - Create visual football field layout
    - Position player cards by role
    - _Requirements: 4.1, 4.2_

  - [ ] 11.5 Add animations and hover effects
    - Add subtle transitions on hover/tap
    - Add loading states and feedback animations
    - _Requirements: 8.5_

  - [ ] 11.6 Implement responsive design
    - Add media queries for mobile/tablet/desktop
    - Ensure touch-friendly tap targets on mobile
    - _Requirements: 1.4, 8.7_

- [-] 12. Wire up league creation functionality
  - [x] 12.1 Connect league creation form to LeagueManager
    - Add form submit handler
    - Validate input and display errors
    - Save league and navigate to home on success
    - _Requirements: 2.2, 2.3, 2.5_

  - [ ] 12.2 Write integration test for league creation flow
    - Test complete flow from form input to storage
    - _Requirements: 2.2, 2.5_

- [ ] 13. Wire up team creation functionality
  - [ ] 13.1 Render player list grouped by role
    - Use PlayerManager to get players by role
    - Generate HTML for each player with selection controls
    - _Requirements: 3.2_

  - [ ] 13.2 Connect player selection to TeamManager
    - Add click handlers for player selection
    - Update budget display in real-time
    - Disable players when budget insufficient or team full
    - _Requirements: 3.3, 3.4, 3.5, 3.6_

  - [ ] 13.3 Connect team creation form submission
    - Validate team name
    - Save team and navigate to team view
    - _Requirements: 3.7_

  - [ ] 13.4 Write property test for player display information
    - **Property 9: Player display contains required information**
    - **Validates: Requirements 4.3**

  - [ ] 13.5 Write integration test for team creation flow
    - Test complete flow from player selection to storage
    - _Requirements: 3.3, 3.7_

- [ ] 14. Wire up team view functionality
  - [ ] 14.1 Load and display user's team
    - Use TeamManager to load saved team
    - Render players on football field by role
    - Display total team score
    - _Requirements: 4.2, 4.3, 4.4_

  - [ ] 14.2 Handle empty team state
    - Display message prompting team creation when no team exists
    - _Requirements: 4.5_

  - [ ] 14.3 Write integration test for team display
    - Test team loading and rendering
    - _Requirements: 4.2, 4.3, 4.4_

- [ ] 15. Wire up ranking functionality
  - [ ] 15.1 Load league and calculate rankings
    - Use LeagueManager to load league
    - Use RankingCalculator to compute rankings
    - Render ranking list with user team highlighted
    - _Requirements: 5.1, 5.2, 5.3_

  - [ ] 15.2 Handle empty league state
    - Display message when no teams exist
    - _Requirements: 5.5_

  - [ ] 15.3 Write integration test for ranking display
    - Test ranking calculation and rendering
    - _Requirements: 5.1, 5.2, 5.3_

- [ ] 16. Implement app initialization
  - [ ] 16.1 Create main initialization function
    - Generate mock players on first load
    - Load saved data from localStorage
    - Initialize navigation
    - Set up all event listeners
    - _Requirements: 7.3_

  - [ ] 16.2 Add error handling for initialization failures
    - Handle localStorage unavailable
    - Handle corrupted data gracefully
    - _Requirements: 7.4_

  - [ ] 16.3 Write property test for immediate storage updates
    - **Property 19: Storage updates are immediate**
    - **Validates: Requirements 7.5**

- [ ] 17. Final checkpoint - End-to-end testing
  - Ensure all tests pass, ask the user if questions arise.
  - Manually test complete user flows:
    - Create league → Create team → View team → View ranking
  - Verify data persists across page reloads
  - Test on multiple browsers and screen sizes

- [ ] 18. Code cleanup and documentation
  - [ ] 18.1 Add JSDoc comments to all functions
    - Document parameters, return values, and behavior
    - _Requirements: 9.2_

  - [ ] 18.2 Add inline code comments for complex logic
    - Explain algorithms and business rules
    - _Requirements: 9.2_

  - [ ] 18.3 Review and refactor for code quality
    - Remove unused code
    - Ensure consistent naming conventions
    - Verify separation of concerns
    - _Requirements: 9.4_

## Notes

- All tasks are required for comprehensive coverage
- Each task references specific requirements for traceability
- Checkpoints ensure incremental validation at key milestones
- Property tests validate universal correctness properties across many inputs
- Unit tests validate specific examples and edge cases
- Integration tests verify components work together correctly
- The implementation follows a layered approach: data → logic → UI
- All core functionality is implemented before styling for faster iteration
