---
description: Debug and fix issues with systematic testing, bug reproduction, and root cause analysis
argument-hint: <issue or problem description>
allowed-tools: [Read, Write, Edit, Grep, Bash, Agent, TodoWrite]
---

# Testing and Debugging

You are helping debug and fix issues in the codebase. Follow a systematic approach to reproduce, analyze, and fix problems.

## Core Principles

- **Systematic**: Reproduce the issue first, then identify root cause
- **Incremental**: Make small changes and test
- **Root cause focus**: Fix the actual problem, not just symptoms
- **Test-driven**: Write tests to verify fixes

---

## Phase 1: Issue Analysis and Reproduction

**Goal**: Understand and reproduce the issue

Input: $ARGUMENTS

**Actions**:
1. Create a todo list to track debugging progress
2. Analyze the issue description
3. Reproduce the bug:
   - If a bug report, follow the steps to reproduce
   - Ask for more information if needed
4. Capture detailed error information (stack traces, logs)
5. Identify when and where the issue occurs

---

## Phase 2: Root Cause Analysis

**Goal**: Find the actual problem, not just symptoms

**Actions**:
1. Explore relevant code and data:
   - Search for error messages or related files
   - Check recent changes that might have introduced the issue
2. Identify the root cause:
   - Use debugging techniques to isolate the problem
   - Check for boundary conditions and edge cases
3. Determine:
   - Why it's happening
   - What's the expected behavior
   - What's the actual behavior

---

## Phase 3: Fix Implementation

**Goal**: Implement a fix for the issue

**Actions**:
1. Based on root cause, fix the issue:
   - Make minimal, focused changes
   - Follow existing coding patterns
2. Write tests to prevent regression
3. Verify the fix:
   - Reproduce the scenario and confirm it's fixed
   - Check if the fix breaks other functionality
4. Document the fix in the commit message

**Fix Guidelines**:
- Keep it simple and focused
- Write a clear commit message explaining the problem and solution
- Add tests to prevent regression
- If the fix is complex, consider refactoring

---

## Phase 4: Regression Testing

**Goal**: Ensure the fix doesn't break anything else

**Actions**:
1. Run all tests
2. Check related functionality
3. Verify the fix works in all environments
4. Check if there are any performance impacts
5. Confirm with the user that the issue is resolved

---

## Phase 5: Documentation and Closure

**Goal**: Complete the debugging process

**Actions**:
1. Mark todos complete
2. Document the issue and fix:
   - What was the problem?
   - How was it reproduced?
   - What was the root cause?
   - How was it fixed?
   - What tests were added?
3. If working on a bug tracker, update the issue with fix details
4. Thank the user for their assistance and confirm the issue is resolved

---

## Best Practices

1. **Reproduce first**: Always reproduce the issue before attempting to fix
2. **Isolate the problem**: Narrow down to the specific code causing the issue
3. **Fix the root cause**: Don't just patch the symptom - fix the underlying issue
4. **Write tests**: Add tests to prevent the issue from happening again
5. **Check for similar issues**: Look for related bugs or potential regressions
6. **Keep it simple**: Make minimal changes to fix the issue
7. **Document everything**: Keep track of what you did and why

---

## Debugging Techniques

### Common Techniques
- **Print debugging**: Add debug statements to track flow
- **Logging**: Check existing logs for clues
- **Error messages**: Look at error messages and stack traces
- **Code review**: Review recent changes for potential issues
- **Incremental testing**: Make small changes and test
- **Hypothesis testing**: Form hypotheses and verify them

### Tools
- Grep: Search codebase for patterns
- Read: Read relevant files
- Edit: Make changes to fix issues
- Bash: Run commands and tests
- Agent: Explore large codebases

---

## Output Format

Keep the user informed of your debugging process:
- What you're investigating
- What you've tried
- What you've found
- What you're planning to fix
- The final solution

Mark todos complete as you finish tasks.
