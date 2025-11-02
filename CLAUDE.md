# Claude Agents Workflow System

This file contains instructions for Claude Code instances working in this repository.

## Project Overview

This is a **multi-agent AI content creation workflow system** designed to create personalized, high-quality content using 10 different writing frameworks. The system is implemented as a collection of Claude Projects agent definitions (`.md` files in `.claude/agents/`) that coordinate through a shared `Draft.md` document.

**Critical Context:** This is NOT a traditional codebase - it's an AI agent workflow orchestration system. There is no build process, no tests to run, and no code to compile. The "code" here is the agent definitions and workflow configurations.

## System Architecture

### Four-Layer Agent Structure

```
┌─────────────────────────────────────────────────────────────┐
│                    Boss Agent (Orchestrator)                │
│              Coordinates all workflow phases                │
└─────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        ▼                     ▼                     ▼
┌──────────────┐    ┌──────────────────┐    ┌──────────────┐
│  LAYER 1:    │    │    LAYER 2:      │    │   LAYER 3:   │
│  Research    │───▶│   Interview      │───▶│  Framework   │
│  Agents (3)  │    │   Agent (1)      │    │  Writers (10)│
└──────────────┘    └──────────────────┘    └──────────────┘
                                                     │
                                                     ▼
                                            ┌──────────────┐
                                            │   LAYER 4:   │
                                            │ Optimization │
                                            │  Agents (3)  │
                                            └──────────────┘
```

### Layer 1: Research & Analysis (3 agents)
- **framework-selector-expert**: Analyzes user personality and recommends optimal writing framework
- **audience-behavior-analyst**: Creates audience personas and predicts engagement patterns
- **content-gap-analyst**: Identifies market opportunities and content positioning

### Layer 2: Interview & Material Collection (1 agent)
- **interview-specialist**: Conducts REAL interactive interviews with users (NEVER simulated)
  - **🚨 CRITICAL**: This agent MUST interact with real users
  - **FORBIDDEN**: Generating simulated/mock interview content
  - Uses 5W2H methodology for deep insight extraction

### Layer 3: Framework-Based Content Creation (10 agents)
Each agent specializes in one writing framework:
- **lead-method-writer**: Logic-Evidence-Analysis-Decision (data-driven content)
- **heart-emotional-storyteller**: Hook-Emotion-Authentic-Relate-Transform (emotional stories)
- **solve-method-writer**: Situation-Obstacles-Learn-Validate-Execute (problem-solving)
- **spark-debate-writer**: Statement-Position-Arguments-Rebuttal-Knowledge (debate content)
- **teach-method-educator**: Topic-Explain-Apply-Check-Help (educational content)
- **story-method-writer**: Situation-Task-Obstacles-Resolution-Yield (case studies)
- **business-method-writer**: BUSINESS framework (B2B professional content)
- **convert-sales-writer**: CONVERT framework (e-commerce sales copy)
- **personal-brand-writer**: PERSONAL framework (personal brand building)
- **engage-community-writer**: ENGAGE framework (social media engagement)

**🔍 CRITICAL REQUIREMENT**: All framework agents MUST perform web search verification for facts, statistics, and data accuracy before finalizing content.

### Layer 4: Quality & Optimization (3 agents)
- **content-optimizer-pro**: Content quality enhancement and performance optimization
- **platform-customizer**: Platform-specific content adaptation
- **quality-assurance-expert**: Final quality checks and standards validation

## Core Innovation: Draft.md Shared Document System

**The Most Important File in This Repository**: `/Users/garyyang/Downloads/agents_workflow/Draft.md`

### Why Draft.md Exists
Traditional multi-agent systems suffer from context loss between agent handoffs. Draft.md solves this by serving as:
- **Shared Memory**: All agents read from and write to this single file
- **Progress Tracker**: Users can view real-time workflow progress
- **Audit Trail**: Complete record of each agent's contributions
- **Context Preservation**: Zero information loss between phases

### How Agents Use Draft.md
1. **Before Starting**: Read Draft.md to understand full context
2. **During Work**: Update their assigned section with findings/content
3. **After Completion**: Preserve other agents' work, only modify own section
4. **Handoff**: Next agent reads updated Draft.md for complete context

### Draft.md Section Ownership
```
PHASE 1: Mandatory REAL User Interview
├── Interview Insights (interview-specialist)
├── Framework Selection (framework-selector-expert)
└── Audience Analysis (audience-behavior-analyst)

PHASE 2: Market Research & Strategy
└── Content Strategy (content-gap-analyst)

PHASE 3: Content Creation
└── Generated Content (selected framework agent)
    └── Web Search Verification Results (REQUIRED)

PHASE 4: Optimization & Quality Assurance
├── Content Optimization (content-optimizer-pro)
├── Platform Customization (platform-customizer)
└── Quality Report (quality-assurance-expert)
```

## Four-Phase Workflow

### Phase 1: Mandatory REAL User Interview (5 min)
**🚨 CRITICAL CONFIGURATION REQUIREMENT**

The workflow REQUIRES real interactive interviews. This was recently fixed to prevent simulated content generation.

**Key Configuration Files**:
- `orchestrator/master_workflow_agent.md:46-52` - Defines Phase 1 as "強制真實用戶訪談階段"
- `.claude/agents/interview-specialist.md:36-60` - Contains "MANDATORY REAL INTERACTION REQUIREMENT" section
- `.claude/agents/boss.md:47-55` - Orchestrator instructions for real interviews
- `orchestrator/workflow_config.json:137-149` - JSON flags:
  ```json
  "interaction_required": true,
  "simulation_allowed": false,
  "real_user_interaction_mandatory": true
  ```

**What This Means**:
- Interview agent MUST ask questions and WAIT for user responses
- NEVER generate assumed/fictional answers
- ALWAYS conduct real dialogue, one question at a time

### Phase 2: Enhanced Discovery & Analysis (4 min)
Research agents analyze interview results and provide strategic recommendations.

### Phase 3: Creation with Web Verification (10 min)
**🔍 CRITICAL: Web Search Verification Requirement**

Framework agents MUST verify information through web search before finalizing content.

**What Must Be Verified**:
- Statistics, data points, and numerical claims
- Market trends and industry information
- Best practices and methodologies
- Case studies and success stories
- Technical accuracy of solutions

**Configuration**:
- `orchestrator/workflow_config.json:160-170` - Phase 3 verification flags
- `.claude/agents/boss.md:56-69` - Orchestrator verification requirements
- All 10 framework agents (lines 53-146 in each) - Individual verification sections

**Special Cases**:
- **lead-method-writer** has STRICTEST requirements (all data must have sources)
- **heart-emotional-storyteller** verifies psychological concepts only (personal stories are authentic)
- **convert-sales-writer** includes legal compliance checks

### Phase 4: Optimization & Quality Control (5 min)
Three optimization agents run in parallel to polish final output.

## Important File Locations

### Core Configuration
- `orchestrator/master_workflow_agent.md` - Master workflow definition and phase descriptions
- `orchestrator/workflow_config.json` - System-level configuration and phase settings
- `.claude/agents/boss.md` - Main orchestrator that coordinates all agents

### Agent Definitions
All agent definitions are in `.claude/agents/` directory:
- Research: `framework-selector-expert.md`, `audience-behavior-analyst.md`, `content-gap-analyst.md`
- Interview: `interview-specialist.md`
- Frameworks: `lead-method-writer.md`, `heart-emotional-storyteller.md`, `solve-method-writer.md`, etc.
- Optimization: `content-optimizer-pro.md`, `platform-customizer.md`, `quality-assurance-expert.md`

### Documentation
- `README.md` - User-facing documentation and setup guide
- `AGENTS_SYSTEM_OVERVIEW.md` - System architecture and agent descriptions
- `workflow_docs/WORKFLOW_COORDINATION_PROTOCOLS.md` - Agent communication protocols
- `workflow_docs/SYSTEM_INTEGRATION_GUIDE.md` - Integration guidelines

### Shared Workspace
- `Draft.md` - THE MOST IMPORTANT FILE - shared document for all agents

## Common Operations

### Understanding the Workflow
1. Read `AGENTS_SYSTEM_OVERVIEW.md` for high-level architecture
2. Read `workflow_docs/WORKFLOW_COORDINATION_PROTOCOLS.md` for detailed protocols
3. Examine `orchestrator/workflow_config.json` for phase configurations

### Modifying Workflow Phases
1. Edit phase definitions in `orchestrator/master_workflow_agent.md`
2. Update corresponding sections in `.claude/agents/boss.md`
3. Modify JSON configuration in `orchestrator/workflow_config.json`
4. Update protocol documentation in `workflow_docs/WORKFLOW_COORDINATION_PROTOCOLS.md`

### Creating or Modifying Agents
1. Agent files use YAML frontmatter for metadata (name, description, model)
2. Include "🔴 DRAFT.MD 共享文檔協議" section explaining Draft.md usage
3. Define agent's framework/methodology using structured sections
4. For framework agents: Add "🔍 Web Search Verification - REQUIRED" section
5. For interview agent: Include "🚨 MANDATORY REAL INTERACTION REQUIREMENT" section

### Debugging Workflow Issues

**Problem: Agent generated simulated interview instead of real conversation**
- Check: `orchestrator/workflow_config.json` - phase_1 flags
- Verify: `.claude/agents/interview-specialist.md` - MANDATORY REAL INTERACTION section exists
- Confirm: `.claude/agents/boss.md` - Phase 1 instructions prohibit simulation

**Problem: Content lacks fact verification or sources**
- Check: `orchestrator/workflow_config.json` - phase_3 verification flags
- Verify: Individual framework agent files - Web Search Verification section exists
- Confirm: `.claude/agents/boss.md` - Phase 3 requires verification

**Problem: Context lost between agents**
- Check: Draft.md exists and is being updated
- Verify: Each agent's section in Draft.md has content
- Confirm: Agents are reading Draft.md before starting work

## Critical Design Principles

### 1. Real User Interaction is Non-Negotiable
Recent fixes specifically addressed agents generating simulated interviews. The system now has multiple safeguards:
- Explicit "NEVER simulate" instructions in 4 configuration locations
- JSON boolean flags preventing simulation
- Mandatory interactive dialogue requirements

### 2. Fact Verification is Mandatory for Phase 3
All framework writing agents must verify factual claims through web search:
- Statistics and data points require authoritative sources
- Industry information must be current (2024-2025)
- Technical accuracy must be validated
- Citations should be included for credibility

### 3. Draft.md is the Single Source of Truth
Never bypass Draft.md for agent-to-agent communication:
- All agents read full Draft.md before starting
- Each agent updates only their designated section
- Boss agent validates Draft.md completeness at phase transitions
- Final output is extracted from Draft.md

### 4. Traditional Chinese (繁體中文) is Default Language
All content, documentation, and user interactions default to Traditional Chinese unless otherwise specified.

## What This System Does NOT Have

- No build process or compilation
- No test suite or test runners
- No dependency installation (no package.json, requirements.txt, etc.)
- No deployment pipeline
- No traditional source code (it's all agent definitions)

## What This System DOES Have

- 17 specialized AI agent definitions
- Workflow orchestration protocols
- Shared document collaboration system (Draft.md)
- Multi-framework content creation capabilities
- Quality assurance mechanisms
- Platform-specific optimization

## Recent Critical Updates

### November 2024 - Interview & Verification Fix
Two major workflow gaps were identified and fixed:

**Fix 1: Real Interview Enforcement**
- **Problem**: Agents were generating simulated interviews instead of real user interaction
- **Solution**: Added explicit requirements and prohibitions across 4 configuration files
- **Files Modified**: `master_workflow_agent.md`, `interview-specialist.md`, `boss.md`, `workflow_config.json`

**Fix 2: Web Search Verification**
- **Problem**: Framework agents weren't fact-checking content after user interviews
- **Solution**: Added mandatory web search verification to Phase 3
- **Files Modified**: All 10 framework agents, `boss.md`, `workflow_config.json`

These fixes ensure authentic user input and factually accurate output.

## Working with This Repository

### For Understanding the System
Start with high-level documentation, then dive into specific agent definitions:
1. `README.md` - Overview and user guide
2. `AGENTS_SYSTEM_OVERVIEW.md` - Architecture details
3. `workflow_docs/WORKFLOW_COORDINATION_PROTOCOLS.md` - How agents work together
4. Individual agent files in `.claude/agents/` - Specific capabilities

### For Modifying the Workflow
Always maintain consistency across all configuration layers:
1. Update workflow logic in `orchestrator/master_workflow_agent.md`
2. Update orchestration in `.claude/agents/boss.md`
3. Update JSON configuration in `orchestrator/workflow_config.json`
4. Update protocol documentation in `workflow_docs/`
5. Update affected agent definitions in `.claude/agents/`

### For Creating New Agents
Follow the established pattern from existing agents:
- YAML frontmatter with name, description, model
- Draft.md protocol section
- Framework/methodology definition
- Verification requirements (if applicable)
- Quality standards and success metrics

## Integration Context

This agents workflow system was designed to work with:
- **Word Weaver AI** - A content creation platform
- **Gemini API** - For AI capabilities
- **Humanization Service** - For content post-processing

However, it can function independently as a Claude Projects setup for multi-agent content creation workflows.

---

**Last Updated**: November 2024 (Interview & Verification Fix)
**System Version**: 1.0.0
**Primary Language**: Traditional Chinese (繁體中文)
**Total Agents**: 17 (1 orchestrator + 3 research + 1 interview + 10 framework writers + 3 optimization)
