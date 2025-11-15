# Issue Analysis Report

## Closed Issues by Category

- bug
  - #50: Cross-project hook inheritance executes sibling project hooks inappropriately (labels: bug, has repro, platform:macos, area:tools)
  - #48: Claude Code executes wrong project hooks in multi-project workspace (labels: bug, has repro, platform:macos, area:tools)
  - #37: Invalid JSON Encoding in API Request Body (labels: bug, duplicate, area:core, platform:macos, area:api)
  - #32: Calling MCP tool create-spec-doc freezes in Cursor AI + GPT-5 (labels: bug, area:mcp, area:ide, external)
  - #25: Missing Tool Result Block for Tool Use ID toolu_01GUUUdR6TqtrqKTprMSuLqc (labels: bug, duplicate, area:core, platform:macos, area:api)
  - #22: Search/Grep tool is BROKEN (labels: bug, has repro, area:tools)
  - #21: Invalid JSON Encoding Error During API Request (labels: bug, duplicate, area:core, platform:macos, area:api)
  - #15: Hard to trace changes in releases (labels: bug)
  - #13: Agent Command Autocomplete Regression in v72 (labels: bug, has repro, platform:macos, area:tui)
  - #12: PowerLevel10k theme causes timeouts and parsing failures (labels: bug, has repro, area:core, platform:macos, area:tui)

- documentation
  - #39: Slash command frontmatter table is misformatted (labels: documentation)
  - #30: Undocumented `statusline` configuration feature (labels: documentation, area:tui)
  - #23: Release notes v1.0.71 not informative (labels: documentation, enhancement)

- enhancement
  - #27: Task color proposal - orange/ginger instead of blue. (labels: enhancement, area:tui)

## Resolution Patterns

- Project-type isolation is a recurring theme:
  - Issues #50 and #48 report cross-project hook execution (Node/npm hooks triggering in Python projects). Root cause appears to be insufficient project context detection and inheritance rules for hooks. Resolution pattern: enforce project-type detection and conditional hook execution.
- API request payload robustness:
  - Issues #37, #25, and #21 are duplicates around invalid JSON encoding and missing tool_result sequencing. Resolution pattern: strengthen JSON serialization, escape handling, and enforce tool_use/tool_result pairing in conversation builders.
- Terminal/ANSI compatibility:
  - Issue #12 highlights ANSI escape contamination from PowerLevel10k. Resolution pattern: strip ANSI/VT control sequences before parsing; detect shell themes and disable conflicting features.
- Tool reliability and indexing:
  - Issue #22 (Grep/Search) indicates mismatch between search tool and actual file contents. Resolution pattern: verify search path roots, indexing strategy, and pattern quoting; add diagnostics for search scope.
- Documentation clarity & release communication:
  - Issues #23, #15, and #30 call for better documentation and release notes. Resolution pattern: expand docs for new features, add changelog entries, and provide concise in-tool change summaries.

## Platform Impact Analysis

- Platform distribution among closed issues indicates macOS predominance:
  - platform:macos present in issues: #50, #48, #37, #25, #21, #13, #12
  - Suggests testing matrix should prioritize macOS terminal ecosystems (Apple Terminal, iTerm2, Cursor, Warp).

## Cross-Project Impact and Memory-Related Problems

- Cross-project impact:
  - #50 and #48 directly affect multi-project workspaces by leaking hooks between language ecosystems, risking spurious failures across projects.
- Memory/encoding-related problems:
  - #37, #21, and #25 involve invalid JSON and message construction issues; these may be exacerbated by large payloads or unescaped control characters, potentially implicating memory pressure or streaming concatenation bugs.

## Notable References

- Related to terminal output sanitation: #12
- Related to search/indexing consistency: #22
- Related to release communications and documentation: #23, #15, #30
