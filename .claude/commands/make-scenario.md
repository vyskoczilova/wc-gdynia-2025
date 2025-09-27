---
allowed-tools: WebFetch, WebSearch, Write, Read, Edit
description: Create Make.com scenario with planning, documentation, and MCP/blueprint implementation
argument-hint: "<scenario-description> [--blueprint-only]"
# Metadata (ignored by Claude Code, but useful for humans)
author: Karolína Vyskočilová <karolina@kybernaut.cz>
created: 2025-09-25
updated: 2025-09-25
---

# Make.com Scenario Creator

Creates cost-effective Make.com scenarios based on your description, with proper planning, implementation via MCP (make-dot-com), and comprehensive documentation.

## Usage
- `/make-scenario "Sync Airtable records to Google Sheets when status changes"`
- `/make-scenario "Process new emails with AI and save to database" --blueprint-only`

## Features
- **Smart Planning**: Analyzes requirements and creates implementation plan
- **Cost Optimization**: Uses single AI requests with structured output parsing
- **MCP Integration**: Implements via Make.com MCP or creates JSON blueprint
- **Clear Documentation**: Generates scenario documentation with technical details
- **Module Clarity**: Uses descriptive names and proper flow organization

## Instructions

### 1. Plan Creation
- Analyze the scenario description for:
  - Required apps and integrations
  - Trigger conditions and frequency
  - Data transformations needed
  - Error handling requirements
  - Cost optimization opportunities
- Create detailed implementation plan
- Present plan to user for approval before implementation

### 2. Make.com Documentation Research
- Fetch current Make.com basics from https://help.make.com/
- Research specific modules from https://apps.make.com/ for required integrations
- Identify optimal module configurations and data mapping

### 3. Cost Optimization Strategy
- Consolidate AI operations into single requests where possible
- Use structured output with [var-name][/var-name] tags for easy regex parsing
- Minimize API calls through efficient data batching
- Suggest webhook triggers over polling when appropriate

### 4. Implementation Options
- **Default**: Create scenario in connected Make.com account via MCP
- **Blueprint Mode** (--blueprint-only): Generate JSON blueprint file only
- Use clear, descriptive module names for debugging
- Implement proper error handling with retry logic

### 5. Documentation Generation
For each created scenario, generate documentation including:
- **Plain Language Summary**: What the scenario accomplishes
- **Scenario Name**: Clear, descriptive identifier
- **Flow Description**: Each module with ID, name, version, mapper data, and metadata
- **Technical Details**: Include builtin and onerror modules
- **Setup Instructions**: Configuration requirements and gotchas

### 6. Quality Assurance
- Verify all modules have appropriate error handling
- Ensure data mapping covers edge cases
- Test scenario logic flow for completeness
- Validate cost-effectiveness of the solution

## Examples

### Good Input
```
"Monitor RSS feed for new posts, extract key points with AI, post summary to Slack channel, and save full analysis to Google Drive"
```

### Generated Plan
1. **RSS Trigger**: Watch RSS feed (polling every 15 min)
2. **Content Filter**: Check for new posts since last run
3. **AI Processing**: Single OpenAI call requesting structured output:
   - [summary]brief summary[/summary]
   - [key_points]bullet points[/key_points]
   - [sentiment]positive/negative/neutral[/sentiment]
4. **Regex Parser**: Extract structured data from AI response
5. **Slack Notification**: Post summary and key points
6. **Google Drive**: Save complete analysis as document
7. **Error Handler**: Log failures, retry logic for API timeouts

## Error Handling
- Invalid scenario description: Request clarification with examples
- Missing MCP connection: Offer blueprint creation instead
- Module not found: Suggest alternatives from Make.com catalog
- Cost concerns: Provide optimization recommendations

## Performance Notes
- Scenarios run efficiently with minimal operations count
- Uses webhook triggers where possible to reduce polling costs
- Batches data operations to minimize API calls
- Includes proper error handling to prevent scenario failures