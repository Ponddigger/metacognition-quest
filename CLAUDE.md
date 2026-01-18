# CLAUDE.md - Metacognition Quest

## Project Overview

Metacognition Quest is a 10-15 minute browser-based educational text adventure game that teaches players about metacognition (thinking about one's own thinking) through gameplay with an AI companion and Socratic reflection pauses.

## Tech Stack

- **Vanilla JavaScript, HTML, CSS only** - no external dependencies
- **Single HTML file deployment** - all code in one `index.html` file
- **No build step required** - open directly in browser

## Visual Design

80s terminal aesthetic:
- Background: black (`#000`)
- Text: green (`#0f0`) or amber (`#ffb000`)
- Font: monospace
- Blinking cursor animation
- Scanline effects optional

## Design Document

**Primary specification:** `metacognition-quest-design.md`

This comprehensive design doc contains all game content, mechanics, and implementation details. Reference it for:
- Exact scenario text and branching logic
- AI companion dialogue patterns
- Socratic question algorithms
- Implementation pseudocode

## Game Architecture

### Game State
```javascript
gameState = {
  currentScenario: 1,
  decisions: [],           // Track all player choices
  aiUsageCount: 0,
  totalDecisions: 0,
  socraticResponses: [],   // Player's reflective answers
  gameComplete: false
}
```

### Game Flow
```
Introduction → Scenario 1 (Archive) → Scenario 2 (Collaboration) →
Socratic Pause 1 → Scenario 3 (Creation) → Socratic Pause 2 → Ending
```

### Core Systems

1. **Command Parser** - Handles player input
   - `ASK [question]` - Consult AI companion (available throughout)
   - Scenario-specific commands: EXPLORE, SCAN, RESPOND, RESEARCH, DEFER, CREATE, DELEGATE, REFUSE

2. **AI Companion** - Never gives direct answers, poses reflective questions back to player

3. **Socratic Pauses** - Two reflection points with dynamically generated questions based on:
   - Player's decision patterns
   - AI usage frequency (high vs. low)
   - Specific choices from decision history

4. **Ending Screen** - Displays:
   - Full decision history with outcomes
   - All Socratic reflections player typed
   - Pattern summary

## Scenarios

### Scenario 1: The Archive
Player chooses how to search ancient knowledge repository:
- EXPLORE - Deep dive into one section
- SCAN - Broad surface-level review
- ASK - Consult AI companion

### Scenario 2: The Collaboration
Colleague requests immediate help on unfamiliar topic:
- RESPOND - Give immediate answer
- RESEARCH - Delay to find information
- ASK - Consult AI companion
- DEFER - Admit uncertainty

### Scenario 3: The Creation
Create artifact under deadline pressure:
- CREATE - Build independently
- COLLABORATE - Co-create with AI
- DELEGATE - Let AI create it
- REFUSE - Decline the task

## Implementation Notes

- Track every decision in `decisions[]` array with choice and outcome
- AI companion consultations increment `aiUsageCount`
- Socratic questions reference actual player decisions by name
- High AI usage = 2+ consultations, Low = 0-1
- Player types free-form responses during Socratic pauses

## Testing

1. Open `index.html` in browser
2. Play through all three scenarios
3. Test each branching path
4. Verify ASK command works at every point
5. Check Socratic pauses show correct dynamic questions
6. Confirm ending displays full history
