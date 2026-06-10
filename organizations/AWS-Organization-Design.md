# Enterprise AWS Organization Design & Governance Rationales
ROOT (Management Account)
├── Security OU
│   ├── Audit Account
│   └── Log Archive Account
├── Infrastructure OU
│   ├── Shared Services
│   └── Networking
├── Production OU
│   ├── Banking-App
│   └── Customer-App
├── Non-Production OU
│   ├── Development
│   └── Testing
└── Sandbox OU
