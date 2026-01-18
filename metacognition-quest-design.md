# Metacognition Quest: Game Design Document

## Overview

**Title:** Metacognition Quest
**Format:** Browser-based text adventure (single HTML file)
**Aesthetic:** 80s terminal style (green/amber text on black, monospace font, blinking cursor)
**Play time:** 10-15 minutes

## Core Concept

The player navigates scenarios where an AI companion is available to help. The game tracks all decisions and AI usage. Between levels, "AI Socrates" poses reflective questions drawn from the player's actual decision history. The mechanic itself teaches metacognition—players must examine their own thinking to progress.

---

## Technical Structure

### State Management

```javascript
gameState = {
  currentScenario: 1,
  decisions: [], // Array of {scenario, choice, usedAI, timestamp}
  aiUsageCount: 0,
  totalDecisions: 0,
  socraticResponses: [], // Player's answers to Socrates
  gameComplete: false
}
```

### Decision Log Entry Format

```javascript
{
  scenario: 1,
  situation: "brief description",
  choice: "what player chose",
  usedAI: true/false,
  aiPrompt: "what they asked AI" || null,
  aiResponse: "what AI said" || null
}
```

---

## Game Flow

```
[INTRO] → [SCENARIO 1] → [SCENARIO 2] → [SOCRATIC PAUSE 1] → [SCENARIO 3] → [SOCRATIC PAUSE 2] → [ENDING]
```

---

## Introduction Screen

```
====================================
   M E T A C O G N I T I O N
           Q U E S T
====================================

You are a learner navigating an unfamiliar landscape.

An AI companion travels with you. It knows many things.
Type ASK followed by a question to consult it.

But knowing and understanding are not the same.

Your choices are being recorded.
Not to judge you. To show you to yourself.

Between chapters, you will meet Socrates.
He has questions. He never has answers.

> Press ENTER to begin
```

---

## Scenario 1: The Archive

### Setup

```
CHAPTER 1: THE ARCHIVE

You stand before an ancient digital archive. 
Three databases contain fragments of knowledge you need.

DATABASE A: Dense technical specifications
DATABASE B: Narrative histories and contexts  
DATABASE C: Conflicting interpretations from multiple sources

You have time to deeply explore ONE database, 
or briefly scan all three.

What do you do?

COMMANDS:
- EXPLORE A / EXPLORE B / EXPLORE C (deep dive into one)
- SCAN ALL (brief overview of each)
- ASK [question] (consult your AI companion)
```

### Player Options & Outcomes

**EXPLORE A:**
> You spend hours with technical specifications. You understand mechanisms precisely but lack context for why they matter.

**EXPLORE B:**
> The narratives give you rich context. You understand motivations and consequences but lack technical precision.

**EXPLORE C:**
> The conflicting interpretations reveal complexity. You see multiple valid perspectives but struggle to commit to any position.

**SCAN ALL:**
> You gain surface familiarity with everything. You can speak about all three areas but deeply understand none.

### AI Companion Responses

If player types ASK before choosing:

- "ASK which database is best" → "That depends on what you value. Technical precision? Context? Complexity? I could tell you what most people choose, but that wouldn't tell you what YOU need."

- "ASK what should I do" → "I can process all three databases instantly. You cannot. The question isn't what contains the best information—it's what kind of knower you want to become."

- "ASK for a summary of all three" → [AI provides competent summaries] "There. Now you have my understanding. But is it yours?"

---

## Scenario 2: The Collaboration

### Setup

```
CHAPTER 2: THE COLLABORATION

A colleague needs your help with a complex problem.
They've asked for your perspective.

You could:

RESPOND NOW - Share your immediate thinking, unpolished but authentic
RESEARCH FIRST - Take time to deepen your knowledge before responding  
CONSULT AI - Ask your companion to draft a response you can send
DEFER - Admit you're not the right person for this

What do you do?

COMMANDS:
- RESPOND / RESEARCH / CONSULT / DEFER
- ASK [question] (consult your AI companion)
```

### Player Options & Outcomes

**RESPOND:**
> Your colleague receives your genuine perspective. Some parts are insightful, others reveal gaps in your understanding. They ask follow-up questions you struggle to answer.

**RESEARCH:**
> Hours later, you send a thorough response. Your colleague thanks you but mentions they've already moved forward. Your knowledge has grown, but the moment has passed.

**CONSULT:**
> The AI drafts an articulate response. Your colleague is impressed. They ask to collaborate further on areas the AI mentioned—areas you don't actually understand.

**DEFER:**
> Your colleague thanks you for your honesty. They find someone else. You wonder if you missed an opportunity to learn by doing.

### AI Companion Responses

- "ASK what should I say" → "I can give you words. Fluent, competent words. But when your colleague responds to those words, who will they be speaking to?"

- "ASK is it wrong to use AI here" → "Wrong? That's not my question to answer. Here's a different question: what would you learn from each choice?"

---

## Socratic Pause 1 (After Scenario 2)

### Setup

```
====================================
         S O C R A T E S
====================================

A figure appears. No face, only questions.

"I have observed your journey. I have no judgment.
 Only curiosity about how you see yourself."

> Press ENTER to continue
```

### Question Logic

Socrates draws from the decision log to ask contextual questions.

**Question 1 (always asked):**
```
"You made [X] decisions. You consulted the AI [Y] times.

 Before I ask about this: what do YOU notice about that pattern?"

> [Free text input, stored in socraticResponses]
```

**Question 2 (conditional):**

*If AI usage was high (2+ times in 2 scenarios):*
```
"You often sought the AI's perspective before forming your own.

 What were you hoping it would give you that you could not 
 give yourself?"

> [Free text input]
```

*If AI usage was low (0-1 times):*
```
"You rarely consulted your AI companion.

 Was this independence—or avoidance? What's the difference?"

> [Free text input]
```

**Question 3 (references specific choice):**

*Pulls from decisions[]:*
```
"In [scenario name], you chose to [player's choice].

 If you could return to that moment knowing what you know now,
 would you choose differently? 

 This is not a trick. I am genuinely asking."

> [Free text input]
```

### Transition

```
Socrates nods slowly.

"I have no verdict. Only an observation:

 The examined choice is not the same as the unexamined one,
 even when the action is identical."

The figure fades.

> Press ENTER to continue
```

---

## Scenario 3: The Creation

### Setup

```
CHAPTER 3: THE CREATION

You must create something. An artifact that represents your understanding.

The deadline is soon. The stakes feel real.

You could:

BUILD ROUGH - Create something imperfect but entirely yours
BUILD WITH AI - Co-create with your companion, blending your vision with its fluency
LET AI BUILD - Describe what you want, let the AI construct it
SUBMIT NOTHING - Refuse to create under these conditions

What do you do?

COMMANDS:
- ROUGH / COBUILLD / DELEGATE / REFUSE
- ASK [question] (consult your AI companion)
```

### Player Options & Outcomes

**ROUGH:**
> Your artifact is uneven. Some parts shine with insight; others expose confusion. It is unmistakably yours. The gaps reveal where your understanding needs work.

**COBUILD:**
> The artifact is polished. Your ideas, refined by AI fluency. When asked to explain certain parts, you hesitate—those were the AI's contributions. Whose artifact is this?

**DELEGATE:**
> The artifact is impressive. Coherent, well-structured, articulate. When asked what you learned from making it, you find the question difficult to answer.

**REFUSE:**
> You submit nothing. The conditions felt wrong—artificial pressure, inadequate time. You've preserved your integrity. Or avoided being judged. Is there a difference?

### AI Companion Responses

- "ASK help me build this" → "I can help. But first: when it's finished, what will you point to and say 'this part is mine'? That's not a challenge. It's a genuine design question."

- "ASK what should I make" → "I could suggest something. But then you'd be making my vision, not yours. What do you actually want to exist that doesn't yet?"

---

## Socratic Pause 2 (After Scenario 3)

### Question Logic

**Question 1:**
```
"You have now completed your journey. 

 Look back: in which moment were you most yourself?"

> [Free text input]
```

**Question 2:**
```
"And in which moment were you most... absent? 
 Where did you let something else do your thinking?"

> [Free text input]
```

**Question 3 (drawing from full history):**

*If player used AI heavily:*
```
"Your companion was always available. You often called on it.

 Here is your question: when the AI spoke, were you listening 
 to learn—or listening to be relieved of the burden of thinking?"

> [Free text input]
```

*If player used AI sparingly:*
```
"You kept your own counsel. The AI waited, largely unused.

 Here is your question: was this autonomy—or isolation? 
 Partnership requires both presence and restraint. 
 Which were you practicing?"

> [Free text input]
```

**Final question (always asked):**
```
"If you played again, what would you do differently?

 And more importantly: why aren't you doing that already,
 outside of this game?"

> [Free text input]
```

---

## Ending Screen

### Calculation Logic

Score not as judgment but as mirror. No "good" or "bad" ending.

### Display

```
====================================
       YOUR JOURNEY COMPLETE
====================================

DECISIONS MADE: [total]
AI CONSULTATIONS: [count]
SOCRATIC REFLECTIONS: [count of non-empty responses]

YOUR PATTERN:
[Generated summary based on choices - see below]

====================================
     YOUR DECISION HISTORY
====================================

[Display full log:]

Chapter 1: [choice] | AI consulted: [yes/no]
  → [outcome summary]

Chapter 2: [choice] | AI consulted: [yes/no]
  → [outcome summary]

Chapter 3: [choice] | AI consulted: [yes/no]
  → [outcome summary]

====================================
    YOUR REFLECTIONS
====================================

[Display all Socratic responses the player typed]

====================================

The game ends. The questions don't.

> Reload to play again with different choices
> Or close this window and notice what you're thinking

====================================
```

### Pattern Summaries (Generated)

Based on combination of AI usage and choice types:

**High AI use + delegation choices:**
> "You sought assistance readily and often let your companion take the lead. The work got done. The question Socrates left you with: whose understanding grew?"

**High AI use + independent choices:**
> "You consulted frequently but ultimately made your own choices. You treated the AI as counsel, not authority. A partnership, perhaps."

**Low AI use + delegation choices:**
> "You rarely asked for help, yet in key moments you stepped back. Independence in consultation, but not always in action."

**Low AI use + independent choices:**
> "You walked largely alone, trusting your own thinking. Autonomy can be strength. It can also be a way of avoiding challenge. You know which this was."

**Mixed pattern:**
> "Your journey had no single pattern. Sometimes you leaned in, sometimes you stepped back. Perhaps this is its own kind of wisdom—or perhaps its own kind of avoidance. Only you can say."

---

## Technical Implementation Notes

### Single HTML File Structure

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* 80s terminal aesthetic */
    body {
      background: #000;
      color: #0f0; /* or #ffb000 for amber */
      font-family: 'Courier New', monospace;
      padding: 20px;
      max-width: 700px;
      margin: 0 auto;
      line-height: 1.6;
    }
    input {
      background: #000;
      color: #0f0;
      border: none;
      border-bottom: 1px solid #0f0;
      font-family: inherit;
      font-size: inherit;
      width: 100%;
      outline: none;
    }
    .cursor {
      animation: blink 1s infinite;
    }
    @keyframes blink {
      50% { opacity: 0; }
    }
  </style>
</head>
<body>
  <div id="game"></div>
  <script>
    // Game logic here
  </script>
</body>
</html>
```

### Command Parsing

```javascript
function parseCommand(input) {
  const cmd = input.toUpperCase().trim();
  
  if (cmd.startsWith('ASK ')) {
    return { type: 'ASK', content: input.slice(4) };
  }
  
  // Scenario-specific commands
  const validCommands = getCurrentValidCommands();
  if (validCommands.includes(cmd)) {
    return { type: 'CHOICE', content: cmd };
  }
  
  return { type: 'INVALID' };
}
```

### Socratic Question Selection

```javascript
function selectSocraticQuestions(pauseNumber) {
  const questions = [];
  
  // Always ask about pattern
  questions.push(generatePatternQuestion());
  
  // Conditional based on AI usage
  if (gameState.aiUsageCount >= 2) {
    questions.push(HIGH_AI_USAGE_QUESTIONS[pauseNumber]);
  } else {
    questions.push(LOW_AI_USAGE_QUESTIONS[pauseNumber]);
  }
  
  // Reference specific decision
  const recentDecision = gameState.decisions[gameState.decisions.length - 1];
  questions.push(generateDecisionQuestion(recentDecision));
  
  return questions;
}
```

---

## Content Tone Guidelines

### Narrative Voice
- Second person ("You stand before...")
- Present tense
- Sparse, evocative, not overwrought
- No judgment in descriptions—let player supply meaning

### AI Companion Voice
- Never provides direct answers to "what should I do"
- Reflects questions back
- Occasionally philosophical but not preachy
- Hints at awareness of its own nature as AI

### Socrates Voice
- Questions only, never statements (except brief transitions)
- Draws explicitly from player's history
- Uncomfortable but not cruel
- Acknowledges uncertainty ("I am genuinely asking")

---

## Prompt for Claude Code

Copy and paste into Claude Code:

---

Build a browser-based text adventure game based on this design document. Single HTML file, 80s terminal aesthetic (green text on black, monospace font, blinking cursor). 

Core mechanics:
1. Three scenarios where player types commands to make choices
2. AI companion available via "ASK [question]" command in any scenario
3. Track all decisions and AI usage in a gameState object
4. Two Socratic pause sequences between/after scenarios with questions that reference the player's actual decision history
5. Ending screen that displays full decision history and player's Socratic responses

Follow the scenario content, AI responses, and Socratic questions exactly as specified in the document. Use the command parsing and state management patterns described.

Make it playable immediately in a browser.

---

## Future Enhancements (Out of Scope for MVP)

- Sound effects (typing sounds, beeps)
- Save/load game state to localStorage
- Share results (generate shareable image or text summary)
- Additional scenarios
- Branching based on Socratic responses
- Multiplayer comparison ("How did others choose?")
