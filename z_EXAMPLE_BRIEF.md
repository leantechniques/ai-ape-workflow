# Old Brief
This brief is an example of what one looked like at the time of it's making. The brief system has evolved for improvements. But the core concept is still comparable.

# Brief 06a: Tokenizer Foundation

**Filename**: `briefs/06a_compiler_tokenizer-foundation.md`
**Created**: 2025-10-23
**Status**: ✅ completed (2025-10-23)

---

## 📋 CURRENT MODE: planning

### Exploration Decision (2025-10-23): ✅ COMPLETE (from Brief 06)
**Parent Brief**: Brief 06 exploration determined tokenizer + recursive descent parser approach
**Rationale**: Walking skeleton validated, production parser needed for Briefs 07/08/15

### Required Reading:
- [ ] docs/context/MISSION.md
- [ ] docs/workflow/planning-mode.md
- [ ] [Project-specific architectural decisions if applicable]
- [ ] [Project-specific technical references if applicable]
- [ ] [Relevant source files to understand current implementation]

### Architecture Tags:
- #compiler
- #tokenizer
- #lexical-analysis
- #render-section
- #stage-2-phase-1
- #foundation

---

## Intent

**What outcome are we after and why?**

**Build the tokenizer (lexical analyzer)** to convert render section text into a stream of tokens for parsing.

**Why**: The walking skeleton uses regex parsing (render-generator.js), but production compiler needs structured token stream for:
- Recursive parsing (nested `when`, `each`, components)
- Precise error messages (line/column positions)
- Clean separation: lexical analysis → parsing → code generation

**Outcome**:
- Can tokenize: `when props.x [Text:Display<content: {props.label}>]`
- Token stream includes: `WHEN`, `IDENTIFIER`, `BRACKET_OPEN`, component names, props, etc.
- Token positions tracked (line/column) for error messages

**Context**:
- Brief 06 split into 06a (tokenizer), 06b (parser), 06c (codegen+validation), 06d (integration)
- This is Phase A: Foundation for all subsequent work
- Briefs 07/08/15 will extend this tokenizer (add `each`, `as`, slots)

---

## Constraints

**What must remain true no matter what?**

**Mission alignment**:
- Tokenizer is foundation for compile-time constraint enforcement
- Token positions enable precise pedagogical error messages (ADR-016)
- Zero Svelte/React patterns in tokenizer (novel syntax only)

**Technical constraints**:
- Single-pass character scanner (no backtracking)
- Token types cover entire render section syntax (not just `when`)
- Location tracking: line, column, start/end positions
- Error handling: Invalid characters should be tokenizable (parser handles semantics)

**Token types needed** (for Brief 06 + future):
- **Keywords**: `WHEN`, `EACH`, `AS` (Brief 07)
- **Delimiters**: `ANGLE_OPEN` (`<`), `ANGLE_CLOSE` (`>`), `BRACKET_OPEN` (`[`), `BRACKET_CLOSE` (`]`), `PAREN_OPEN` (`(`), `PAREN_CLOSE` (`)`), `PIPE` (`|`)
- **Identifiers**: `NAMESPACE_NAME` (Text:Display), `IDENTIFIER` (props.x)
- **Expressions**: `EXPRESSION` (contents of `{...}`)
- **Literals**: `STRING`, `NUMBER`
- **Special**: `COLON`, `COMMA`, `WHITESPACE`, `NEWLINE`, `EOF`

**Syntax constraints**:
- Render syntax (not JavaScript, not HTML)
- Handle expressions `{...}` as opaque strings (parser validates later)
- Whitespace-insensitive (track but don't error on spacing)

---

## Signal

**How will we know this is right?**

**Primary signal - Token stream correctness**:
1. Input: `when props.x [Text:Display]`
2. Tokens: `[WHEN, IDENTIFIER(props.x), BRACKET_OPEN, NAMESPACE_NAME(Text:Display), BRACKET_CLOSE, EOF]`
3. Each token has location: `{ line: 1, column: 5, start: 4, end: 9 }`

**Secondary signals - Test coverage**:
- Can tokenize keywords: `when`, `each`, `as`
- Can tokenize component names: `Text:Display`, `Section:Box`
- Can tokenize props: `content: {props.label}`
- Can tokenize nested structures: `when x [when y [Text:Display]]`
- Can track positions correctly (multi-line input)
- All 328 existing tests still pass (no regressions)

**Test signals**:
- 30+ tokenizer tests pass
- Can handle edge cases: empty input, whitespace-only, long expressions
- Invalid characters tokenize (don't crash)

**Failure signals**:
- Tokens missing location info
- Can't tokenize multi-line input
- Expressions not captured correctly
- Delimiter confusion (angle vs bracket)

---

## Success Criteria

**Tokenizer succeeds if**:
1. ✅ Can tokenize `when` conditionals
2. ✅ Can tokenize component usage with props
3. ✅ Can tokenize nested structures
4. ✅ Token positions accurate (line/column)
5. ✅ Handles expressions `{...}` as opaque tokens
6. ✅ 30+ tokenizer tests pass
7. ✅ All 328 existing tests still pass
8. ✅ No regressions in current validation/compilation

**Measurement deliverables**:
- [ ] 30-35 tokenizer tests (token-types.test.js, tokenizer.test.js)
- [ ] Token type constants file (token-types.js)
- [ ] Character scanner implementation (tokenizer.js)
- [ ] README for tokenizer explaining design

**Decision point**:
- **If successful**: Proceed to Brief 06b (parser)
- **If partial**: Simplify token types or improve scanner
- **If unsuccessful**: Re-evaluate tokenization approach

**Timebox**: 6-8 hours (0.75-1 day)

---

## Implementation Notes

### **New Files to Create**

**Token Types**:
- `src/compiler/token-types.js` - Token type constants (WHEN, BRACKET_OPEN, etc.)
- `test/compiler/token-types.test.js` - Token type enumeration tests (5-8 tests)

**Tokenizer**:
- `src/compiler/tokenizer.js` - Character scanner, tokenization logic
- `test/compiler/tokenizer.test.js` - Tokenizer tests (25-30 tests)

**Documentation**:
- `src/compiler/README.md` - Tokenizer design notes

### **Files to Reference** (not modify yet):
- `src/compiler/render-generator.js` - Current regex approach (will be replaced in 06b)

### **Implementation Phases**

**Phase A: Token Type Definitions**
1. [ ] Define token type constants (WHEN, BRACKET_OPEN, etc.)
2. [ ] Create token constructor/helper functions
3. [ ] Write token type tests (5-8 tests)
4. [ ] **Run tests**: Verify token types work
5. [ ] **Commit**: "Brief 06a Phase A: Token type definitions"
6. [ ] **STOP**: End session, resume at Phase B

**Phase B: Character Scanner**
7. [ ] Write Test: Tokenize single keyword (`when`)
8. [ ] Implement: Basic scanner loop + keyword detection
9. [ ] Write Test: Tokenize delimiters (`[`, `]`, `<`, `>`)
10. [ ] Implement: Delimiter tokenization
11. [ ] Write Test: Tokenize component names (`Text:Display`)
12. [ ] Implement: Namespace:Name pattern detection
13. [ ] Write Test: Tokenize expressions (`{props.x}`)
14. [ ] Implement: Expression capture (brace balancing)
15. [ ] Write Test: Tokenize props (`content: {value}`)
16. [ ] Implement: Prop tokenization (colon, comma)
17. [ ] **Run tests**: Verify all scanner tests pass
18. [ ] **Commit**: "Brief 06a Phase B: Character scanner implementation"
19. [ ] **STOP**: End session, resume at Phase C

**Phase C: Location Tracking**
20. [ ] Write Test: Tokens have line/column positions
21. [ ] Implement: Position tracking in scanner
22. [ ] Write Test: Multi-line input positions correct
23. [ ] Implement: Newline handling
24. [ ] Write Test: Token start/end positions
25. [ ] Implement: Offset tracking
26. [ ] Write Test: Complex nested structure positions
27. [ ] Implement: Position preservation through nesting
28. [ ] **Run tests**: Verify all position tests pass (30+ total)
29. [ ] **Commit**: "Brief 06a Phase C: Location tracking complete"
30. [ ] **STOP**: End session, resume at validation

**Phase D: Validation & Regression**
31. [ ] Run full test suite (328 existing + 30 new = 358 total)
32. [ ] Verify no regressions in validators
33. [ ] Verify no regressions in existing compiler
34. [ ] Manual test: Tokenize example component
35. [ ] **Commit**: "Brief 06a complete: Tokenizer foundation (358 tests passing)"
36. [ ] Create ghost file: `ghosts/2025-10-23-brief-06a.md`
37. [ ] Update Brief 06a status → completed
38. [ ] **STOP**: Brief 06a complete, ready for Brief 06b

---

## Open Questions for Planning Mode

1. **Token type organization**: Single file or multiple? (Preference: Single `token-types.js`)
2. **Expression handling**: Capture entire `{...}` or tokenize contents? (Preference: Opaque string)
3. **Whitespace strategy**: Token type or skip? (Preference: Skip but track positions)
4. **Error handling**: How to handle invalid characters? (Preference: Create ERROR token, continue)
5. **Test organization**: One file or split by concern? (Preference: Split - types vs tokenizer)

---

## 🔍 Integration Audit (Required Before Completion)

**✅ COMPLETED** (2025-10-23)

### Error Codes & Documentation
- [x] **New error codes?** → N/A (Brief 06a is foundation, no errors yet)
- [x] **Changed error format?** → N/A
- [x] **Error examples work?** → N/A

### CLI Integration
- [x] **New commands?** → No (CLI unchanged)
- [x] **Changed command behavior?** → No
- [x] **CLI output format changed?** → No

### Reference Documentation
- [x] **New syntax?** → No (tokenizer is internal)
- [x] **Changed behavior?** → No
- [x] **New patterns?** → No
- [x] **All examples compile?** → N/A (no user-facing changes)

### Examples Directory
- [x] **New feature?** → No (internal tooling)
- [x] **Changed syntax?** → No
- [x] **Examples build?** → N/A
- [x] **Example README?** → N/A

### Test Organization
- [x] **New test fixtures?** → Yes → ✅ Verified in `test/compiler/` (tokenizer.test.js, token-types.test.js)
- [x] **New test files?** → Yes → ✅ Follow naming convention (tokenizer.test.js, token-types.test.js)
- [x] **Test fixtures documented?** → N/A (unit tests, not fixtures)

### Architecture Documentation (if applicable)
- [x] **Implementation diverged from ADR?** → ✅ No - Matches ADR-012 exactly (hand-rolled tokenizer, returns tokens with type/value/line/column)
- [x] **New architectural pattern?** → No
- [x] **Changed existing pattern?** → No

**Notes for Brief 06a**:
- Tokenizer is internal compiler component (no user-facing changes)
- Most checklist items N/A (CLI, examples, reference docs unchanged)
- Focus: Test organization ✅, verify ADR-012 alignment ✅

**Integration Audit Result**: ✅ PASS - All requirements met

---

## 📝 PLANNING OUTPUT

**Planning Status**: ✅ COMPLETE (2025-10-23)

### Goal
Build a character-by-character scanner that tokenizes render section syntax into a structured token stream with accurate position tracking for error messages.

### Success Criteria
1. ✅ Can tokenize keywords (`when`, `each`, `as`)
2. ✅ Can tokenize component names (`Text:Display`, `Section:Box`)
3. ✅ Can tokenize all delimiters (`[`, `]`, `<`, `>`, `{`, `}`, `(`, `)`, `|`)
4. ✅ Can tokenize expressions (`{props.count + 1}`) as opaque strings
5. ✅ Can tokenize props (`content: "value"`, `count: {expr}`)
6. ✅ Token positions are accurate (line, column, start, end)
7. ✅ 30-35 new tokenizer tests pass
8. ✅ All 358 existing tests still pass (no regressions)

### Dependencies

**Phase A (Foundation)**:
- Task 1 → Task 2 → Task 3 (sequential token type definition)
- Can be completed in single session

**Phase B (Scanner Core)**:
- Requires: Phase A complete (token types defined)
- Task 8 → Task 9 (keywords before identifiers)
- Task 10 → Task 11 (delimiters before component names)
- Task 12 → Task 13 (component names before expressions)
- Task 14 → Task 15 (expressions need brace balancing)
- Task 16 → Task 17 (props need all previous features)
- Each test-implement pair builds on previous (sequential within phase)

**Phase C (Position Tracking)**:
- Requires: Phase B complete (basic scanner working)
- Task 19 → Task 20 (position tracking foundation)
- Task 21 → Task 22 (newline handling extends position tracking)
- Task 23 → Task 24 (offset tracking extends both)
- Task 25 → Task 26 (complex structures test full integration)
- Sequential (each extends previous position tracking feature)

**Phase D (Validation & Integration)**:
- Requires: Phase C complete (tokenizer feature-complete)
- Tasks 27-30 can run in parallel (independent validation checks)
- Task 31 must be last (final commit after all validation passes)

### Tasks

#### Phase A: Token Type Definitions (1 hour)
1. [x] **Write Test**: Token type constants exported correctly (WHEN, BRACKET_OPEN, EOF, etc.)
2. [x] **Implement**: Create `src/compiler/token-types.js` with all token type constants
3. [x] **Write Test**: Token constructor creates valid token objects with type, value, position
4. [x] **Implement**: Create `createToken()` helper function
5. [x] **Run tests**: Verify all token type tests pass (~5-8 tests)
6. [x] **Commit**: "Brief 06a Phase A: Token type definitions"
7. [x] **STOP**: End session, resume at Phase B

#### Phase B: Character Scanner (3-4 hours)
8. [x] **Write Test**: Tokenize single keyword `when` → [WHEN, EOF]
9. [x] **Implement**: Basic scanner loop with keyword detection
10. [x] **Write Test**: Tokenize all keywords (`when`, `each`, `as`) → correct tokens
11. [x] **Implement**: Keyword recognition with lookahead
12. [x] **Write Test**: Tokenize delimiters (`[`, `]`, `<`, `>`, `:`, `,`) → delimiter tokens
13. [x] **Implement**: Delimiter tokenization (single character tokens)
14. [x] **Write Test**: Tokenize component names (`Text:Display`, `Action:Button`) → NAMESPACE_NAME tokens
15. [x] **Implement**: Namespace:Name pattern detection (scan until whitespace/delimiter)
16. [x] **Write Test**: Tokenize expressions (`{props.x}`, `{count + 1}`) → EXPRESSION tokens
17. [x] **Implement**: Expression capture with brace balancing (nested braces support)
18. [x] **Write Test**: Tokenize props (`content: "value"`, `count: {expr}`) → prop tokens sequence
19. [x] **Implement**: Prop tokenization (identifier, colon, value)
20. [x] **Write Test**: Tokenize complete `when` statement with component and props
21. [x] **Implement**: Integration of all scanner features
22. [x] **Run tests**: Verify all scanner tests pass (~20-25 tests total) - 9 new tests, 375 total passing
23. [x] **Commit**: "Brief 06a Phase B: Character scanner implementation"
24. [ ] **STOP**: End session, resume at Phase C

#### Phase C: Position Tracking (2-3 hours)
25. [x] **Write Test**: Tokens have line/column positions (line: 1, column: 5)
26. [x] **Implement**: Position tracking in scanner (track line/column during scan)
27. [x] **Write Test**: Multi-line input positions correct (newlines increment line, reset column)
28. [x] **Implement**: Newline handling (detect `\n`, update line/column)
29. [x] **Write Test**: Token start/end positions (start: 0, end: 4 for "when")
30. [x] **Implement**: Offset tracking (character positions in source string)
31. [x] **Write Test**: Complex nested structure positions accurate
32. [x] **Implement**: Position preservation through all tokenization paths
33. [x] **Run tests**: Verify all position tests pass (~30-35 tests total)
34. [x] **Commit**: "Brief 06a Phase C: Location tracking complete"
35. [ ] **STOP**: End session, resume at validation

#### Phase D: Validation & Integration (30-45 min)
36. [x] Run full test suite (380 total - all passing)
37. [x] Verify no regressions in validators (Brief 01-05 tests)
38. [x] Verify no regressions in existing compiler (render-generator still works)
39. [x] Manual test: Tokenize example component from test fixture
40. [x] **Commit**: "Brief 06a Phase D validation: All 380 tests passing"
41. [x] Create ghost file: `ghosts/2025-10-23-brief-06a.md`
42. [x] Update Brief 06a status → completed in brief file
43. [x] **STOP**: Brief 06a complete, ready for Brief 06b


---

### Implementation Approach

**Files to Create**:
- `src/compiler/token-types.js` - Token type constants and createToken() helper
- `src/compiler/tokenizer.js` - Tokenizer class with character scanning logic
- `test/compiler/token-types.test.js` - Token type definition tests (5-8 tests)
- `test/compiler/tokenizer.test.js` - Tokenizer scanning tests (25-30 tests)

**Token Types Needed**:
- Keywords: WHEN, EACH, AS
- Delimiters: BRACKET_OPEN/CLOSE, ANGLE_OPEN/CLOSE, BRACE_OPEN/CLOSE, PAREN_OPEN/CLOSE, PIPE
- Identifiers: NAMESPACE_NAME (Text:Display), IDENTIFIER (props.x, item)
- Values: EXPRESSION (contents of {...}), STRING, NUMBER
- Special: COLON, COMMA, WHITESPACE, NEWLINE, EOF

**Tokenizer Design**:
- Single-pass character scanner (no backtracking)
- Track position: line, column, start offset, end offset
- Whitespace: skip but maintain accurate positions
- Expressions: capture entire {...} as opaque string with brace balancing
- Component names: detect Namespace:Name pattern
- Keywords: distinguish from identifiers using lookahead

**Testing Strategy**:
- Phase A: Token type constants and helper functions (5-8 tests)
- Phase B: Character scanning for all token types (20-25 tests)
- Phase C: Position tracking accuracy (5-8 tests)
- Phase D: Regression testing (358 existing tests)

---

### Open Questions Resolved

1. **Token type organization**: Single file `token-types.js` (simpler, easier to import)
2. **Expression handling**: Capture entire `{...}` as opaque string (parser validates later)
3. **Whitespace strategy**: Skip whitespace, but track positions accurately
4. **Error handling**: For Brief 06a, tokenize everything (parser handles semantic errors in Brief 06b)
5. **Test organization**: Split - `token-types.test.js` for types, `tokenizer.test.js` for scanner

---

### Risk Assessment

**Plan**: 43 tasks across 4 phases (A: Token types, B: Scanner, C: Position tracking, D: Validation)

**Risks**:
- ⚠️ **Expression brace balancing** (nested braces) - Medium complexity
- ⚠️ **Position tracking correctness** - Must handle newlines correctly
- ✅ Low risk overall - tokenization is well-understood domain

**Next Brief After 06a**:
- Brief 06b: Recursive descent parser (uses token stream from tokenizer)

---

**Last Updated**: 2025-10-23
**Status**: Planning complete, ready for implementation
**Next**: Await explicit approval to commit plan

