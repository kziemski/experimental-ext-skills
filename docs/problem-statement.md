# Problem Statement

Native "skills" support in host applications demonstrates demand for rich workflow instructions, but there's no convention for exposing equivalent functionality through MCP primitives.

## Current Limitations

- **Server instructions load only at initialization** — new or updated skills require re-initializing the server
- **Complex workflows exceed practical instruction size** — some skills require hundreds of lines of markdown with references to bundled files, scripts, and examples
- **No discovery mechanism** — users installing MCP servers from a registry don't know if there's a corresponding skill they should also install
- **Multi-server orchestration** — skills may need to coordinate tools from multiple servers, which doesn't fit the single-server instruction model

## Key Use Cases

### 1. Complex Workflow Orchestration

Bob Dickinson's [mcpGraph](https://github.com/TeamSparkAI/mcpGraph) toolkit requires a skill file of 875+ lines to instruct agents on building directed graphs of MCP nodes. This orchestration logic is "way more than you'd want to put in instructions."

### 2. Conditional Workflows

Workflows that reference tools conditionally based on context, requiring rich structured instructions that can be dynamically loaded.

### 3. Multi-Server Composition

Skills that leverage tools from multiple off-the-shelf servers where you can't (or don't want to) modify their individual instructions.

### 4. Progressive Disclosure

Skills broken into linked sets of files for effective context management, loaded progressively as the agent needs them rather than all at once.

## Open Questions

1. **Is this a registry problem or an MCP server problem?** Should skills be discoverable through registry metadata ("if you install this server, also install this skill") or contained within the MCP server itself?

2. **How do "first-class" skills differ from "skills as context"?** Native agent skills can be presented through the user agent, bundled with subagents, etc. Do MCP-surfaced skills lose capabilities compared to directly installed skills?

3. **Should server.instructions be extended for richer content?** Or is the separation between "primitive server" and "skill that uses the primitive" the right abstraction?

4. **How should skills relate to multiple servers?** A skill orchestrating tools from several servers can't live in any single server's instructions.

5. **Do clients actually leverage skills when presented via MCP?** Early experiments suggest they do, but more rigorous testing is needed.

6. **How do we coordinate with agent skills spec owners?** The contribution model for the skills spec isn't clear, and MCP-related efforts should be brought to their attention.

7. **What would MCP have had to get right for skills to have been shipped over MCP from the beginning?** (https://github.com/keithagroves)

8. **What could MCP reasonably change so that it will be the obvious choice for new formats?** (https://github.com/keithagroves)

9. **Who gets visibility into skill content, and who decides when it gets loaded?** The control model question — model-controlled vs. application-controlled. (https://github.com/olaservo)

10. **How should skills handle security and trust boundaries?** If skills can be abused for prompt injection, what mitigations should be spec'd? (provenance, gating, explicit policy) (https://github.com/Agent-Hellboy)

11. **Should the control model be use-case specific?** Perhaps resources (application-controlled) for some use cases, tools (model-controlled) for others? Can a convention support both? (https://github.com/olaservo)
