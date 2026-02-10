# Zoro Agent Architecture: The Mansion

## Overview

The Zoro agent system is architected as a hierarchical mansion structure, where **Zorro** serves as the master orchestrator and head of the household. The mansion operates with specialized agents, each fulfilling distinct roles in a coordinated workflow. This document serves as the complete architectural blueprint for understanding and implementing the Zoro agent ecosystem.

## Architecture Philosophy

The mansion architecture follows a **hierarchical orchestration pattern** where:
- **Zorro** (Primary Agent) operates at the top level using the primary API key
- All sub-agents operate using secondary API keys managed by the Butler
- Each agent has specialized responsibilities and clear communication channels
- Task execution follows a structured workflow from creation to completion
