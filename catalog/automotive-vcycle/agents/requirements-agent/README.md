# Automotive Requirements Analyzer and UAT Generator

The Requirements Analyzer transforms requirements documents into consistency analysis reports and comprehensive user acceptance test specifications for automotive software development.

The automotive requirements analyzer and user acceptance test generator is implemented using Strands Agents framework and deployed on Amazon Bedrock AgentCore Runtime. 


## Architecture

```
┌─────────────────┐    ┌──────────────────────────┐             ┌─────────────────┐
│   MCP Client    │───▶│  AgentCore Runtime       │──generates─▶│  Analysis &     │
│(requirements-   │    │  Requirements Agent      │             │  User Acceptance│
│    server)      │    │  (Strands)               │             │  Tests          │
└─────────────────┘    └──────────────────────────┘             └─────────────────┘
```

- **Agent**: Requirements analysis and UAT generation
- **Framework**: Strands Agents with AgentCore Runtime
- **Authentication**: Amazon Cognito with JWT tokens
- **Runtime**: Amazon Bedrock AgentCore Runtime
- **Model**: Nova 2 Lite for analysis and test generation
- **Output**: Requirements validation report and user acceptance test specifications

## Files

- `requirements-analyzer.ipynb` - Main Jupyter notebook demonstrating the multi-agent system
- `requirements_analyzer.py` - Full Strands-based requirements analyzer implementation
- `requirements.txt` - Python dependencies for the agent to be deployed to AgentCore Runtime.


### Path Configuration

The notebook and analyzer are configured to work from the agent directory with the following path structure:

```
catalog/automotive-vcycle/
├── agents/
│   ├── utils.py                                # Shared utility functions for Cognito auth
│   ├── requirements.txt                        # Shared Python dependencies
│   └── requirements-agent/                     # Requirements Analyzer (current directory)
│       ├── requirements-analyzer.ipynb
│       ├── requirements_analyzer.py
│       └── requirements.txt
└── sample-data/weather-app/
    ├── business-requirements/
    │   └── weather_app_brd.md
    └── technical-requirements/
        └── weather_app_srs.md
```

### Key Features

1. **Business Requirements Focus**: Analyzes documents from `../../sample-data/weather-app/business-requirements/`
2. **Multi-Agent Architecture**: Uses Strands agents with conditional execution
3. **AgentCore Runtime**: Deploys to Amazon Bedrock AgentCore Runtime
4. **Authentication**: Integrated with Amazon Cognito for secure access
5. **User Acceptance Tests**: Generates comprehensive test specifications

## Getting Started

### Prerequisites
- Python 3.12+ (see [parent README](../../README.md) for virtual environment setup)
- AWS CLI configured for a US based region
- Amazon Bedrock access
- AgentCore Runtime permissions

### 1. Deploy Infrastructure Interactively (via Notebooks)
This section describes the deployment via notebooks. If you want to deploy via ma3t toolkit, refer to  [parent README](../../README.md)

Run notebook cells. This will deploy the agent to the agentcore runtime.

### 2. Adjust the Settings/Steering Files for Local IDE
- For Kiro, use the files under `./ide-support/kiro` folder (choose files selectively based on your agent).
- For Cline, use `./ide-support/cline`.
- Adjust the Cognito Client-Id from your deployment from step 1.
- Adjust your local path to the `requirements-server.py` if necessary.
- Adjust your Python path if necessary.



### Troubleshooting

If you encounter deployment issues:

1. Ensure all dependencies are installed
2. Check AWS credentials are configured
3. Review the notebook output for specific error messages

For 424 "Failed Dependency" errors, the issue is typically related to:
- Missing dependencies in requirements.txt
- Docker container build failures
- Import errors in the Python code