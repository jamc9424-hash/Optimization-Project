# Optimization-

# Basketball Lineup and Rotation Optimization

A decision support app that helps basketball coaches select five-player lineups and plan substitutions based on the opponent, available players, and game situation.

An independent project inspired by how bad CU basketball is currently playing. Not affiliated with or endorsed by CU Athletics.

## Project Goal

Allow a coach to enter scouting observations, adjust strategic priorities, and receive lineup and rotation recommendations with understandable explanations.

The coach can:
- Select an opponent and describe its strengths and weaknesses.
- Set player availability, minutes limits, and role requirements.
- Lock players into a lineup or exclude them.
- Compare recommended lineups and their tradeoffs.
- Update game conditions and request substitution recommendations.
- Override any recommendation.

## Current Stage

Planning and mathematical formulation. The first task is to define the inputs, objective, and constraints before expanding implementation.

## Roadmap

### Phase 1 — Define the Coaching Decision

Specify the questions the app should answer:

- Pregame: Which lineups fit this opponent, and how should player minutes be allocated?
- During a game: Given the current five, opposing lineup, fouls, and minutes played, what substitution should we consider next?

Start with manual game updates and a clearly defined planning horizon.

**Deliverable:** Agreed inputs, outputs, and decision scope.

### Phase 2 — Define Player and Opponent Inputs

Create editable data templates covering:

| Category | Example Inputs |
|---|---|
| Player attributes | Shooting, creation, ball security, perimeter defense, interior defense, rebounding |
| Opponent characteristics | Size, pressure, shooting, offensive rebounding, interior scoring, likely lineups |
| Coaching restrictions | Availability, minutes limits, rest requirements, player locks and exclusions |
| Game conditions | Current five, opposing five, score, clock, fouls, minutes played |

Separate measured statistics from subjective scouting ratings. Define consistent rating scales with basketball input.

**Deliverable:** Data dictionary and fictional example inputs.

### Phase 3 — Establish Matchup Scoring

Translate scouting observations and coaching priorities into explicit attribute weights.

Evaluate competing responses. For example, a large opponent could justify matching size or using a smaller lineup to create spacing.

Initially, use an explainable weighted scouting score. This represents coaching preferences, not predicted points or win probability.

**Deliverable:** Documented scoring assumptions and worked examples.

### Phase 4 — Formulate Single-Lineup Optimization

Use binary player-selection variables to choose exactly five players.

Include constraints for:
- Player availability.
- Required role coverage.
- Coach locks and exclusions.
- Any mandatory lineup characteristics.

Distinguish hard requirements from preferences that can be traded against other benefits.

Begin with a binary linear model. Enumerate feasible five-player combinations as an exact benchmark for validating the solver.

**Deliverable:** Mathematical formulation and verified lineup recommendations.

### Phase 5 — Extend to Rotations and Substitutions

Use player-by-stint decisions in Gurobi to plan a sequence of lineups.

Account for:
- Remaining player minutes.
- Consecutive playing time and required rest.
- Role coverage in every stint.
- Players entering and leaving.
- A coaching preference for lineup continuity.

Reoptimize after updates while preserving actual minutes played and existing play/rest history. Planned stint boundaries approximate legal substitution opportunities.

**Deliverable:** Feasible rotation plan, player minutes totals, and substitution explanations.

### Phase 6 — Build the Coach Interface

Provide three main views:

| View | Main Actions |
|---|---|
| Prepare matchup | Enter opponent observations and adjust priorities |
| Manage roster | Set availability, minutes limits, and player selections |
| Review recommendations | Compare lineups, inspect rotations, and update game conditions |

Show alternatives, score differences, strengths, weaknesses, and the restrictions driving each recommendation.

Explain conflicting requirements when no feasible lineup or rotation exists.

**Deliverable:** Interactive prototype using fictional data and manual updates.

### Phase 7 — Incorporate Verified Historical Data

Select suitable data sources and document coverage and usage terms.

Reconstruct lineups and possessions, reconcile player participation with recorded minutes, and document data quality.

Keep private scouting, medical information, credentials, and restricted datasets out of the public repository.

**Deliverable:** Reproducible data preparation and quality checks.

### Phase 8 — Evaluate Predictive Models and Player Interactions

Explore opponent-adjusted, regularized performance estimates.

Add player-pair interactions through quadratic terms or their linear equivalents only when supported by evidence.

Evaluate using:
- Chronological training and testing.
- Simple comparison baselines.
- Sample sizes and uncertainty.
- Sensitivity to changes in ratings and priorities.

Historical replay cannot establish what would have happened with a lineup that was never played.

**Deliverable:** Evidence of whether learned estimates improve on the initial scouting scores.

### Phase 9 — Review With Basketball Staff

Demonstrate historical scenarios, collect feedback and overrides, and revise assumptions.

Confirm applicable bench technology and data policies before live use. Add automatic live feeds after manual operation is useful and reliable.

**Deliverable:** Reviewed pilot and a decision on further development.

## Immediate Next Step

Agree on player rating definitions, opponent attributes, and mandatory coaching constraints before expanding implementation.
