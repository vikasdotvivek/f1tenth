# Code improvement triage

**Automated first pass, not a complete manual code audit or a safety certification.**

Repository: `vikasdotvivek/f1tenth`
Snapshot: `a11f3b60c9f304413fc061dcf65cf837d5adf996`

- Tracked paths: 138; source files inspected: 63.
- Findings: 3; retained: 3; omitted by cap: 0.
- Priority counts in retained findings: {'P1': 2, 'P2': 1}.
- No repository code, tests, builds or hardware were executed.

## Scope and limitations

Python findings use AST parsing under the runner Python 3. C/C++/C# findings are lexical review candidates, not compiler-verified defects. Files over 1 MB, designer files, generated/vendor paths, binaries, notebooks, PDFs and other non-source formats are excluded and enumerated in the JSON report. No findings does not establish correctness.

## Build and test follow-up

Build/dependency entry points detected:
- `gap_follow/CMakeLists.txt`
- `gap_follow/package.xml`
- `gap_follow/setup.py`
- `lqr/CMakeLists.txt`
- `lqr/package.xml`
- `lqr/setup.py`
- `mpc/CMakeLists.txt`
- `mpc/package.xml`
- `mpc/setup.py`
- `particle_filter/deprecated/CMakeLists.txt`
- `particle_filter/package.xml`
- `particle_filter/setup.py`
- `pure_pursuit/CMakeLists.txt`
- `pure_pursuit/package.xml`
- `pure_pursuit/setup.py`
- `rrt/CMakeLists.txt`
- `rrt/package.xml`
- `rrt/setup.py`
- `safety_node/CMakeLists.txt`
- `safety_node/package.xml`
Additional entry points are listed in JSON.

Conventional test paths were detected; review their coverage and run the documented suite in the proper environment.

## Potential improvements

### 1. P1: Does not parse with the audit runner Python 3
Source: [particle_filter/deprecated/src/particle_filter.py:128](https://github.com/vikasdotvivek/f1tenth/blob/a11f3b60c9f304413fc061dcf65cf837d5adf996/particle_filter/deprecated/src/particle_filter.py#L128)
Confirm the intended Python version. This may be legacy Python 2 rather than an unintended syntax error; compile with the supported interpreter.

### 2. P1: Does not parse with the audit runner Python 3
Source: [rrt/setup.py:26](https://github.com/vikasdotvivek/f1tenth/blob/a11f3b60c9f304413fc061dcf65cf837d5adf996/rrt/setup.py#L26)
Confirm the intended Python version. This may be legacy Python 2 rather than an unintended syntax error; compile with the supported interpreter.

### 3. P2: Exception handler only passes
Source: [waypoint_logger/scripts/waypoint_logger_node.py:73](https://github.com/vikasdotvivek/f1tenth/blob/a11f3b60c9f304413fc061dcf65cf837d5adf996/waypoint_logger/scripts/waypoint_logger_node.py#L73)
Decide whether the error is recoverable; surface nonrecoverable failures instead of silently continuing.

## Acceptance gate

Confirm each candidate in its calling context. Add a regression test, make one focused change, and build using the actual target dependencies. For robotics/actuator firmware, verify safe outputs, limit handling, sensor failure and timing on a controlled test rig. Do not merge or deploy a blanket rewrite based on these pattern matches.

Machine-readable scope, exclusions and findings: `static-review.json`.
