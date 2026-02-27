# NPO: Narrative Pacing Operator Skill

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill for optimizing narrative prose pacing through intelligent pattern-based culling. Part of the [NSL (Narrative Spittoon Language)](https://github.com/MushroomFleet) ecosystem.

## Overview

NPO strategically culls excessive descriptive prose from narrative chapters and pages — reducing reader cognitive load while preserving all dialogue, pivotal content, and the author's voice. It analyzes the emotional arc, content type, and structure of each chapter, then applies one of five pacing patterns to control where culling is aggressive vs. gentle.

NPO is a **subtraction tool, not a rewriter**. It removes excess. It never adds content or changes what the text says — only how much of it remains.

## Live Web App

A standalone web application version of the NPO system is available at:

**[spittoon.oragenai.com](https://spittoon.oragenai.com/)**

The web app provides a guided wizard interface for the same NPO culling workflow, powered by OpenRouter LLM integration.

## Installation

Download `npo.skill` from this repository and place it in your Claude Code commands directory:

```
# Copy the .skill file
cp npo.skill ~/.claude/commands/

# Or on Windows
copy npo.skill %USERPROFILE%\.claude\commands\
```

Claude Code will automatically discover and load the skill on next session start.

## Two Modes

### Cull Mode

Transforms the text — applies pattern-based culling and outputs the modified prose alongside an analysis report and statistics.

**Trigger phrases:** `"using NPO"`, `"NPO cull"`, `"cull this chapter"`, `"optimize pacing"`, `"tighten this prose"`

**Output:** Analysis Report + Culled Text + Summary Statistics

### Assess Mode

Analyzes only — scores five pacing dimensions, identifies specific passages that would be targeted for culling, and provides prioritized recommendations without modifying any text.

**Trigger phrases:** `"NPO assess"`, `"pacing analysis"`, `"diagnose pacing"`, `"assess this chapter"`

**Output:** Analysis Report + Dimension Scores + Segment Analysis + Priority Recommendations

## Five Pacing Patterns

NPO automatically selects the best pattern based on the chapter's emotional arc, core moment location, content type, and narrative position.

```
Sine Wave:          Peak-Middle:        Trough-Middle:
High |  /\  /\      High |    /\        High |\    /|
Cut  | /  \/  \     Cut  |   /  \       Cut  | \  / |
Low  |/        \    Low  |  /    \      Low  |  \/  |
     |__________|         |_______|           |_____|
     Start    End         Start End           Start End

Linear-Rise:        Linear-Fall:
High |        /     High |\
Cut  |      /       Cut  | \
Low  |    /         Low  |   \
     |  /                |     \
     |/________          |_______\
     Start  End          Start   End
```

| Pattern | Best For | Intensity Curve |
|---------|----------|----------------|
| **Sine Wave** | Rhythmic chapters, action with breathing room | light - aggressive - light - aggressive |
| **Peak-Middle** | Central climax, confrontations, revelations | light - aggressive - light |
| **Trough-Middle** | Emotional core, introspection, character depth | moderate - light - moderate |
| **Linear-Rise** | Escalation, building tension, chase sequences | light - moderate - aggressive |
| **Linear-Fall** | De-escalation, aftermath, cooldown | aggressive - moderate - light |

## How It Works

NPO processes each chapter through a four-phase pipeline:

1. **Analysis** — Reads the full text, identifies all dialogue and pivotal moments, assesses the emotional arc, detects content type, locates the core narrative moment
2. **Pattern Application** — Selects the best pacing pattern, divides the chapter into segments, assigns culling intensity per segment
3. **Culling Execution** *(Cull mode only)* — Processes each segment at its assigned intensity, preserving all protected content
4. **Quality Assurance** *(Cull mode only)* — Verifies dialogue preservation, plot coherence, transition quality, and generates statistics

### Three Culling Intensities

| Intensity | Preservation | What Gets Culled |
|-----------|-------------|-----------------|
| **Light** | 80-90% | Redundant adjective chains, overwrought metaphors, obvious repetition |
| **Moderate** | 60-75% | Lengthy descriptions condensed, secondary sensory details, atmospheric prose |
| **Aggressive** | 40-60% | Descriptions to bare minimum, all non-critical technical content, elaborate atmospherics |

### Absolute Preservation Rules

These rules are inviolable across all modes and intensities:

- **Dialogue is sacred** — every word of quoted speech, internal monologue, and reported dialogue is preserved exactly as written
- **Pivotal content is non-negotiable** — plot-advancing beats, character decisions, revelations, and foreshadowing are never removed
- **Voice fidelity** — the author's recognizable style survives the culling process

## NSL Ecosystem Integration

NPO supports [Narrative Spittoon Language (NSL)](https://github.com/MushroomFleet) bucket context for multi-chapter consistency. When an `.nsl` file or extracted bucket data is provided alongside the chapter text, NPO uses:

- **Character profiles** to identify essential vs. decorative character details
- **World descriptions** to distinguish new worldbuilding (preserve) from established details (cullable)
- **Speech styles** to protect intentional character-voice patterns
- **Series metadata** to refine pattern selection based on volume position

The skill works fully without NSL context — it simply enables smarter decisions for series content.

## Assess Mode: Pacing Dimensions

In Assess mode, NPO scores five pacing dimensions on a 1-5 scale:

| Dimension | What It Measures |
|-----------|-----------------|
| **Dialogue Balance** | How well dialogue and prose are balanced |
| **Descriptive Density** | Whether descriptions are proportionate to their importance |
| **Technical Load** | Whether technical detail serves the story or burdens the reader |
| **Atmospheric Weight** | Whether atmosphere enhances immersion or drags pacing |
| **Rhythmic Variety** | Whether pace varies effectively or feels monotonous |

## Skill File Structure

```
npo-skill/
├── SKILL.md                               # Main orchestrator (two mode workflows)
├── README.md                              # Skill overview
├── references/
│   ├── 01-analysis-protocol.md            # Phase 1: Analysis procedure
│   ├── 02-pattern-application-protocol.md # Phase 2: Segmentation + intensity
│   ├── 03-culling-execution-protocol.md   # Phase 3: Per-segment culling rules
│   ├── 04-quality-assurance-protocol.md   # Phase 4: Verification + statistics
│   ├── pacing-patterns.md                 # All 5 patterns with visualizations
│   ├── pattern-detection-algorithm.md     # Decision tree + decision matrix
│   ├── culling-guidelines.md              # Preserve/target rules + examples
│   ├── special-considerations.md          # Edge cases + error recovery
│   ├── output-template-cull.md            # Cull mode output format
│   ├── output-template-assess.md          # Assess mode output format
│   └── nsl-context-guide.md              # NSL integration guide
└── assets/
    └── nsl-1.1-specification.md           # NSL 1.1 specification
```

## Version

- **System**: NPO (Narrative Pacing Operator)
- **Skill Version**: 1.0
- **Compatible with**: NSL 1.1 specification
- **Based on**: Spittoon-Pacing application (2025) + NPO System Prompt v1.0

## License

MIT

## Citation

### Academic Citation

If you use this codebase in your research or project, please cite:

```bibtex
@software{narrative_pacing_operator,
  title = {Narrative Pacing Operator: Intelligent prose culling skill for Claude Code},
  author = {Drift Johnson},
  year = {2025},
  url = {https://github.com/MushroomFleet/narrative-pacing-operator-skill},
  version = {1.0.0}
}
```

### Donate:

[![Ko-Fi](https://cdn.ko-fi.com/cdn/kofi3.png?v=3)](https://ko-fi.com/driftjohnson)
