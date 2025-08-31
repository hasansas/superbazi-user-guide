```txt
📦 project-root
├── 📁 src
│   ├── 📁 config          # Configuration (db, env, etc.)
│   │   ├── db.ts
│   │   └── env.ts
│   │
│   ├── 📁 modules         # Feature-based modules
│   │   ├── 📁 user
│   │   │   ├── user.model.ts       # Sequelize/Mongoose schema
│   │   │   ├── user.service.ts     # Business logic
│   │   │   ├── user.controller.ts  # Request handling
│   │   │   └── user.route.ts       # Route definitions
│   │   │
│   │   ├── 📁 auth
│   │   │   ├── auth.service.ts
│   │   │   ├── auth.controller.ts
│   │   │   └── auth.route.ts
│   │   │
│   │   ├── 📁 bazi-core             # Core: chart + raw data
│   │   │   ├── 📁 domain
│   │   │   │   ├── index.ts
│   │   │   │   ├── types.ts         # Gan/Zhi/PillarName/TimeLayer/Interaction*, DTOs
│   │   │   │   ├── contracts.ts     # FourPillarsInput, TimeLayersInput, ReportType, etc.
│   │   │   │   └── constants.ts     # stems/branches maps, combos, void tables
│   │   │   ├── 📁 i18n
│   │   │   │   ├── en.ts id.ts zh.ts
│   │   │   ├── 📁 services
│   │   │   │   ├── chart.service.ts
│   │   │   │   ├── time-pillars.service.ts
│   │   │   │   ├── interactions.service.ts
│   │   │   │   ├── life-stages.service.ts
│   │   │   │   ├── melodic-five.service.ts
│   │   │   │   ├── symbolic-stars.service.ts
│   │   │   │   ├── void-emptiness.service.ts
│   │   │   │   ├── structures.service.ts
│   │   │   │   └── profiles.service.ts
│   │   │   ├── 📁 controllers
│   │   │   │   └── core.controller.ts
│   │   │   ├── routes.ts            # /v1/bazi/core/*
│   │   │   ├── 📁 utils
│   │   │   │   ├── calendar.util.ts
│   │   │   │   └── pillar.util.ts
│   │   │   └── 📁 __tests__
│   │   │
│   │   ├── 📁 bazi-analyze          # Analysis logic layer
│   │   │   ├── 📁 domain
│   │   │   │   ├── index.ts
│   │   │   │   └── analyze.types.ts
│   │   │   ├── 📁 rules
│   │   │   │   ├── strength.rules.ts
│   │   │   │   ├── structures.rules.ts
│   │   │   │   ├── interactions.rules.ts
│   │   │   │   ├── useful-god.rules.ts
│   │   │   │   ├── climate.rules.ts
│   │   │   │   ├── mediator.rules.ts
│   │   │   │   ├── qi-flow.rules.ts
│   │   │   │   ├── graveyard.rules.ts
│   │   │   │   └── palace.rules.ts
│   │   │   ├── 📁 services
│   │   │   │   ├── day-master-strength.service.ts
│   │   │   │   ├── special-structures.service.ts
│   │   │   │   ├── useful-god.service.ts
│   │   │   │   ├── climate-adjust.service.ts
│   │   │   │   ├── mediator-god.service.ts
│   │   │   │   ├── qi-flow.service.ts
│   │   │   │   ├── graveyard-storage.service.ts
│   │   │   │   ├── interaction-report.service.ts
│   │   │   │   ├── pillar-analysis.service.ts
│   │   │   │   └── calendar-personalization.service.ts
│   │   │   ├── 📁 controllers
│   │   │   │   └── analyze.controller.ts
│   │   │   ├── routes.ts            # /v1/bazi/analyze/*
│   │   │   └── 📁 __tests__
│   │   │
│   │   ├── 📁 bazi-interpretation   # Narrative / Reports
│   │   │   ├── 📁 domain
│   │   │   │   ├── index.ts
│   │   │   │   ├── interpretation.types.ts
│   │   │   │   └── report.types.ts
│   │   │   ├── 📁 knowledgebase
│   │   │   │   ├── 📁 adult
│   │   │   │   ├── 📁 children
│   │   │   │   ├── 📁 twins
│   │   │   │   └── 📁 templates
│   │   │   ├── 📁 mappers
│   │   │   │   └── analysis-to-narrative.map.ts
│   │   │   ├── 📁 services
│   │   │   │   ├── summary.service.ts
│   │   │   │   ├── forecast.service.ts
│   │   │   │   ├── recommendations.service.ts
│   │   │   │   ├── profile-report.service.ts
│   │   │   │   ├── abilities-report.service.ts
│   │   │   │   ├── education-report.service.ts
│   │   │   │   ├── careers-report.service.ts
│   │   │   │   ├── business-report.service.ts
│   │   │   │   ├── wealth-report.service.ts
│   │   │   │   ├── relationship-report.service.ts
│   │   │   │   ├── health-report.service.ts
│   │   │   │   ├── luck-cycle-report.service.ts
│   │   │   │   ├── destiny-stars-report.service.ts
│   │   │   │   └── main-structure-report.service.ts
│   │   │   ├── 📁 controllers
│   │   │   │   └── interpretation.controller.ts
│   │   │   ├── routes.ts            # /v1/bazi/interpretation/*
│   │   │   └── 📁 __tests__
│   │   │
│   │   ├── 📁 profiles
│   │   ├── 📁 calendars
│   │   ├── 📁 reports
│   │   ├── 📁 recommendations
│   │   ├── 📁 consultation
│   │   ├── 📁 access
│   │   └── 📁 bazi                 # Legacy router aggregator
│   │
│   ├── 📁 middlewares     # Custom middlewares
│   │   ├── auth.middleware.ts
│   │   └── error.middleware.ts
│   │
│   ├── 📁 utils           # Helpers, constants, validators
│   │   ├── logger.ts
│   │   └── response.ts
│   │
│   ├── app.ts             # Express app setup
│   └── server.ts          # Entry point
│
├── .env
├── package.json
├── tsconfig.json
└── README.md
```
