# Superbazi — Technical Documentation
Generated: 2025-08-27 17:47

This document describes the architecture, module boundaries, development workflow, path aliases setup, and operational practices for the Superbazi application. It reflects the 3-module split:

- **bazi-core** — deterministic BaZi computations (charts, pillars, raw interactions, datasets)
- **bazi-analyze** — rule engine & scoring (strength, structures, interaction reports, personalized calendar logic)
- **bazi-interpretation** — narratives & forecasts (characters, abilities, careers, wealth, relationship, health, luck cycle, yearly energy)

---

## 1) Tech Stack

- **Frontend/SSR**: Nuxt 3 (TypeScript), Vite
- **Runtime**: Node 20+
- **Package Manager**: pnpm
- **HTTP**: Express/Nitro server routes (module-based)
- **Styles/UI**: Vuetify 3, SCSS
- **State**: Pinia (client)
- **Validation**: Zod for DTOs
- **Testing**: Vitest + Supertest
- **Docs**: Swagger/OpenAPI
- **Code Quality**: ESLint + Prettier
- **Deployment**: PM2

---

## 2) Repository Structure

```txt
src/
  modules/
    bazi-core/
      domain/
        index.ts
        types.ts                 # Gan/Zhi/PillarName/TimeLayer/Interaction*, DTOs
        contracts.ts             # FourPillarsInput, TimeLayersInput, ReportType
        constants.ts             # mapping tables, combos, void tables
      i18n/
        en.ts id.ts zh.ts
      services/
        chart.service.ts         # natal, day master, hidden stems, ten gods (raw)
        time-pillars.service.ts  # luck/annual/monthly/daily/hourly pillars
        interactions.service.ts  # 五合/六合/三合/三会/半合/冲/刑/害/破/伏吟/反吟 (raw)
        life-stages.service.ts   # 12 life stages
        melodic-five.service.ts  # melodic five elements
        symbolic-stars.service.ts# shen sha
        void-emptiness.service.ts# dead empty/void
        structures.service.ts    # 5 structures (raw)
        profiles.service.ts      # 10 profiles (raw counts)
      controllers/
        core.controller.ts
      routes.ts                  # /v1/bazi/core/*
      utils/
        calendar.util.ts
        pillar.util.ts
      __tests__/...

    bazi-analyze/
      domain/
        index.ts
        analyze.types.ts         # InteractionEffect, TransformOutcome, reports
      rules/
        strength.rules.ts
        structures.rules.ts
        interactions.rules.ts
        useful-god.rules.ts
        climate.rules.ts
        mediator.rules.ts
        qi-flow.rules.ts
        graveyard.rules.ts
        palace.rules.ts
      services/
        day-master-strength.service.ts
        special-structures.service.ts
        useful-god.service.ts
        climate-adjust.service.ts
        mediator-god.service.ts
        qi-flow.service.ts
        graveyard-storage.service.ts
        interaction-report.service.ts
        pillar-analysis.service.ts
        calendar-personalization.service.ts
      controllers/
        analyze.controller.ts
      routes.ts                   # /v1/bazi/analyze/*
      __tests__/...

    bazi-interpretation/
      domain/
        index.ts
        interpretation.types.ts
        report.types.ts           # 'adult' | 'children' | 'twins'
      knowledgebase/
        adult/*.kb.ts
        children/*.kb.ts
        twins/*.kb.ts
        templates/*.tmpl.ts
      mappers/
        analysis-to-narrative.map.ts
      services/
        summary.service.ts
        forecast.service.ts
        recommendations.service.ts
        profile-report.service.ts
        abilities-report.service.ts
        education-report.service.ts
        careers-report.service.ts
        business-report.service.ts
        wealth-report.service.ts
        relationship-report.service.ts
        health-report.service.ts
        luck-cycle-report.service.ts
        destiny-stars-report.service.ts
        main-structure-report.service.ts
      controllers/
        interpretation.controller.ts
      routes.ts                   # /v1/bazi/interpretation/*
      __tests__/...

    profiles/                     # user DOB profiles
      controllers/ profiles.controller.ts
      routes.ts                   # /v1/profiles/*
      services/ profiles.service.ts

    calendars/
      controllers/ calendars.controller.ts
      routes.ts                   # /v1/calendars/*
      services/ tong-shu.service.ts personalized.service.ts

    reports/
      controllers/ reports.controller.ts
      routes.ts                   # /v1/reports/*
      services/ report-renderer.service.ts report-delivery.service.ts i18n-transform.service.ts
      templates/ pdf/base.layout.tsx sections/*

    recommendations/
      controllers/ recommendations.controller.ts
      routes.ts                   # /v1/recommendations/*
      services/ recommendations.service.ts

    consultation/
      controllers/ consultation.controller.ts
      routes.ts                   # /v1/consultation/*
      services/ schedule.service.ts booking.service.ts

    access/
      middleware/ role.guard.ts subscriber.guard.ts entitlement.guard.ts
      policies/ menu.policy.ts

    bazi/
      index.ts                    # mounts sub-routers to keep /v1/bazi/* stable

  routes.ts                       # app router (mount modules)
  app.ts                          # server bootstrap
  env.d.ts                        # ambient typing for env

types/
  externals/ lunar-javascript.d.ts

tests/                            # e2e tests (optional)
```

---

## 3) Path Aliases (How-To)

> Nuxt + Vite usually respect TS paths when configured. We define aliases in **tsconfig.json** (IDE + type checking) and mirror them in **nuxt.config.ts** for runtime.

### 3.1 tsconfig.json
```jsonc
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"],
      "@bazi-core/*": ["src/modules/bazi-core/*"],
      "@bazi-analyze/*": ["src/modules/bazi-analyze/*"],
      "@bazi-interpretation/*": ["src/modules/bazi-interpretation/*"],
      "@profiles/*": ["src/modules/profiles/*"],
      "@calendars/*": ["src/modules/calendars/*"],
      "@reports/*": ["src/modules/reports/*"],
      "@consultation/*": ["src/modules/consultation/*"],
      "@access/*": ["src/modules/access/*"]
    },
    "strict": true,
    "moduleResolution": "bundler",
    "types": ["vite/client"]
  },
  "include": ["src", "types", "env.d.ts"]
}
```

### 3.2 nuxt.config.ts (runtime alias)
```ts
// nuxt.config.ts
import { resolve } from 'pathe';

export default defineNuxtConfig({
  alias: {
    "@": resolve(__dirname, "src"),
    "@bazi-core": resolve(__dirname, "src/modules/bazi-core"),
    "@bazi-analyze": resolve(__dirname, "src/modules/bazi-analyze"),
    "@bazi-interpretation": resolve(__dirname, "src/modules/bazi-interpretation"),
    "@profiles": resolve(__dirname, "src/modules/profiles"),
    "@calendars": resolve(__dirname, "src/modules/calendars"),
    "@reports": resolve(__dirname, "src/modules/reports"),
    "@consultation": resolve(__dirname, "src/modules/consultation"),
    "@access": resolve(__dirname, "src/modules/access")
  },
  // If you prefer reading tsconfig paths automatically:
  // vite: { plugins: [tsconfigPaths()] }
});
```

### 3.3 ESLint (import resolver)
```js
// .eslintrc.cjs
module.exports = {
  settings: {
    'import/resolver': {
      typescript: {
        project: ['./tsconfig.json']
      }
    }
  }
};
```

### 3.4 Vitest
```ts
// vitest.config.ts
import { defineConfig } from 'vitest/config';
import tsconfigPaths from 'vite-tsconfig-paths';

export default defineConfig({
  plugins: [tsconfigPaths()],
  test: {
    environment: 'node',
    globals: true
  }
});
```

### 3.5 Usage Example
```ts
import type { FourPillarsInput } from '@bazi-core/domain';
import { score as dmScore } from '@bazi-analyze/services/day-master-strength.service';
import { forecast } from '@bazi-interpretation/services/forecast.service';
```

---

## 4) Development Workflow

1. **Clone & Install**
   ```bash
   pnpm i
   ```
2. **Environment**
   - Copy `.env.example` → `.env` and set values (see §6).
3. **Run Dev**
   ```bash
   pnpm dev
   ```
4. **Build & Start**
   ```bash
   pnpm build && pnpm start
   ```
5. **Test**
   ```bash
   pnpm test
   ```

---

## 5) API Conventions

- **Route Prefixes**
  - `/v1/bazi/core/*`, `/v1/bazi/analyze/*`, `/v1/bazi/interpretation/*`
  - `/v1/profiles/*`, `/v1/calendars/*`, `/v1/reports/*`, `/v1/recommendations/*`, `/v1/consultation/*`
- **Request/Response Shape**
  - Use DTOs (zod) and return standardized envelopes:
    ```ts
    {{ status: 'success', code: 200, data: {{...}} }}
    {{ status: 'error', code: 400, error: {{ message, details? }} }}
    ```
- **Validation**
  - Define zod schemas with `.parseAsync(req.body)` in controllers.
- **Versioning**
  - Keep `/v1` stable; deprecate with headers when needed.

---

## 6) Configuration & Environment

`.env.example`
```bash
NODE_ENV=development
PORT=3000
API_BASE=/v1
LOG_LEVEL=info
```
`env.d.ts`
```ts
interface ImportMetaEnv {{
  readonly API_BASE: string;
  readonly LOG_LEVEL: 'trace'|'debug'|'info'|'warn'|'error'|'fatal';
}}
interface ImportMeta {{
  readonly env: ImportMetaEnv;
}}
```

---

## 7) Security & Access

- **Role/Tier Guards**: `role.guard`, `subscriber.guard`, `entitlement.guard`
- **CORS**: allow only known origins per env
- **Rate Limiting**: per-IP for public endpoints
- **PII**: protect DOB; avoid logging raw payloads

---

## 8) Logging, Errors, and Observability

- **Logger**: pino with request-id correlation
- **Error Handling**: central middleware converts thrown errors → `{{status:'error'}}` envelope
- **Metrics**: basic latency and error counters (optional Prometheus)

---

## 9) Testing

- **Unit**: rules/services in each module (`__tests__`)
- **API**: Vitest + Supertest for controllers
- **Contract**: OpenAPI schema tests for response compatibility

Example:
```ts
import { describe, it, expect } from 'vitest';
import { score } from '@bazi-analyze/services/day-master-strength.service';

describe('DM Strength', () => {{
  it('scores strong charts higher', () => {{
    const result = score(/* mock */);
    expect(result.value).toBeGreaterThan(60);
  }});
}});
```

---

## 10) Documentation (Swagger)

- Mount a `/docs` route serving OpenAPI JSON + Swagger UI
- Tag by module (`BaZi Core`, `BaZi Analyze`, `BaZi Interpretation`, etc.)

---

## 11) Deployment (PM2)

`ecosystem.config.js`
```js
module.exports = {{
  apps: [
    {{
      name: 'superbazi',
      script: '.output/server/index.mjs',
      env: {{ NODE_ENV: 'production', PORT: 3000 }}
    }}
  ]
}};
```
Commands:
```bash
pnpm build
pm2 start ecosystem.config.js
pm2 logs superbazi
```

---

## 12) Coding Standards

- **TypeScript**: `strict: true`
- **ESLint + Prettier**: run on pre-commit
- **Naming**:
  - Services: `*.service.ts`
  - Controllers: `*.controller.ts`
  - Rules: `*.rules.ts`
  - DTOs/Types: under `domain/`

---

## 13) Migration Tips

- Keep legacy `bazi.routes.ts` and forward to new routers during cutover.
- Move all domain types into `@bazi-core/domain/types.ts` and re-export via barrel.
- Update imports to use the path aliases (see §3).

---

## 14) Minimal Controller Example

```ts
// src/modules/bazi-core/controllers/core.controller.ts
import type { Request, Response } from 'express';
import type { FourPillarsInput } from '@bazi-core/domain';
import * as chart from '../services/chart.service';

export async function natal(req: Request, res: Response) {{
  const input = req.body as FourPillarsInput;
  const data = await chart.computeNatal(input);
  return res.json({{ status: 'success', code: 200, data }});
}}
```

---

## 15) Example Rule Wiring (Analyze)

```ts
// src/modules/bazi-analyze/services/day-master-strength.service.ts
import { z } from 'zod';
import type { TimeLayersInput } from '@bazi-core/domain';

export function score(input: TimeLayersInput) {{
  // compute season weight, resources, companion, output, control, etc.
  return {{ value: 72, band: 'Strong', reasons: ['Seasonal support', 'Resource abundant'] }};
}}
```

---

## 16) Example Narrative Mapping (Interpretation)

```ts
// src/modules/bazi-interpretation/mappers/analysis-to-narrative.map.ts
import type { PillarInteractionReport } from '@bazi-analyze/domain';

export function toCharacters(report: PillarInteractionReport) {{
  return {{ traits: ['Driven', 'Methodical'], evidence: ['Strong output', 'Metal support'] }};
}}
```

---

## 17) Useful Scripts (package.json)

```jsonc
{{
  "scripts": {{
    "dev": "nuxt dev",
    "build": "nuxt build",
    "start": "nuxt start",
    "lint": "eslint . --ext .ts,.vue",
    "format": "prettier --write .",
    "test": "vitest run",
    "test:watch": "vitest"
  }}
}}
```

---

## 18) Appendix — Aliases Checklist

- [x] Add **tsconfig.json** paths
- [x] Add **alias** in `nuxt.config.ts`
- [x] Configure ESLint `import/resolver`
- [x] Add `vite-tsconfig-paths` for Vitest tests
- [x] Update imports to `@bazi-*/*`

---

**That’s it.** Keep this file at `docs/TECHNICAL.md` and update alongside module changes.
