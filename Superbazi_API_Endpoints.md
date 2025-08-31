# Superbazi — API Endpoints (Core, Analyze, Interpretation)
Generated: 2025-08-27 19:46

This document lists all endpoints per module with Status, Endpoint, Feature, Description, and User roles.

## bazi-core
| Status | Endpoint | Feature | Description | User |
| --- | --- | --- | --- | --- |
| To Do | /v1/bazi/core/natal | Natal Chart | Compute natal four pillars (Gan/Zhi), Day Master, Hidden Stems, Ten Gods (raw). | regular, practitioner, corporate |
| To Do | /v1/bazi/core/time-pillars | Time Pillars | Compute Luck (DaYun), Annual (Liu Nian), Monthly (Yue Yun), Daily (Ri Yun), Hourly pillars. | regular, practitioner, corporate |
| To Do | /v1/bazi/core/interactions | Raw Interactions | Detect Five Combination, Six Harmony, Three Harmony, Three Meeting, Partial Combination, Clash, Punishment, Harm, Destruction, Fu Yin, Fan Yin. | regular, practitioner, corporate |
| To Do | /v1/bazi/core/ten-gods | Ten Gods (raw) | Map Ten Gods for each stem relative to Day Master (no scoring). | regular, practitioner, corporate |
| To Do | /v1/bazi/core/life-stages | 12 Life Stages | Compute 12 Life Stages per pillar. | regular, practitioner, corporate |
| To Do | /v1/bazi/core/melodic-five | Melodic Five Elements | Return Melodic Five Elements classification. | regular, practitioner, corporate |
| To Do | /v1/bazi/core/symbolic-stars | Symbolic Stars (Shen Sha) | Compute Shen Sha / destiny stars (raw list). | regular, practitioner, corporate |
| To Do | /v1/bazi/core/void-emptiness | Void/Emptiness | Compute 'Death of Emptiness / Void' positions. | regular, practitioner, corporate |
| To Do | /v1/bazi/core/structures | Five Structures (raw) | Return 5 Structures dataset without interpretation. | regular, practitioner, corporate |
| To Do | /v1/bazi/core/profiles | 10 Profiles (raw) | Return 10 Profiles counts, percentages (no narrative). | regular, practitioner, corporate |

## bazi-analyze
| Status | Endpoint | Feature | Description | User |
| --- | --- | --- | --- | --- |
| To Do | /v1/bazi/analyze/day-master-strength | Day Master Strength | Score DM strength (0–100), band, reasons. Regular requires subscription. | regular, practitioner, corporate |
| To Do | /v1/bazi/analyze/special-structures | Special Structure Admission | Detect Cong/Follow/Fake Cong/etc. with rationale. Regular requires subscription. | regular, practitioner, corporate |
| To Do | /v1/bazi/analyze/useful-god | Useful/Favorable/Unfavorable/Enemy/Idle Gods | Determine Yong/Xi/Ji/Chou/Xian Shen. Regular requires subscription. | regular, practitioner, corporate |
| To Do | /v1/bazi/analyze/climate-adjust | Climate Adjusting God | Tiao Hou Yong Shen (temperature/humidity normalization). | regular, practitioner, corporate |
| To Do | /v1/bazi/analyze/mediator-god | Mediator God | Tong Guan Yong Shen (bridge/mediator evaluation). | regular, practitioner, corporate |
| To Do | /v1/bazi/analyze/qi-flow | Five Element Qi Flow | Evaluate elemental circulation/flow patterns. | regular, practitioner, corporate |
| To Do | /v1/bazi/analyze/graveyard-storage | Graveyard / Storage (Mu/Ku) | Identify storage/graveyard effects and impact. | regular, practitioner, corporate |
| To Do | /v1/bazi/analyze/interaction-report | Interaction Report (scored) | Aggregate raw interactions → effects, intensity, transform confidence. | regular, practitioner, corporate |
| To Do | /v1/bazi/analyze/pillar-analysis | Pillar Analysis | Per-pillar analysis (Year/Month/Day/Hour) with palace context. | regular, practitioner, corporate |
| To Do | /v1/bazi/analyze/palace-context | Contextual Analysis by Palaces | Auxiliary palaces and contextual insights. | regular, practitioner, corporate |
| To Do | /v1/bazi/analyze/calendar/personalized | Personalized BaZi Calendar | Daily tags/scores based on analysis. Regular requires subscription. | regular, practitioner, corporate |

## bazi-interpretation
| Status | Endpoint | Feature | Description | User |
| --- | --- | --- | --- | --- |
| To Do | /v1/bazi/interpretation/summary | Executive Summary | Top findings synthesized from analysis. Regular requires subscription. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/report/characters | Characters | Narrative traits with evidence. Regular requires subscription. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/report/abilities | Abilities | Strengths & capability profile. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/report/education | Education | Learning style & education guidance. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/report/careers | Careers | Career alignment and roles. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/report/business | Business | Business orientation & fit. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/report/wealth | Wealth | Wealth patterns & strategies. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/report/relationship | Relationship | Relationship dynamics. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/report/health | Health | Health tendencies & care tips. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/forecast | Yearly Energy Forecast | Year → months narrative forecast. Regular requires subscription. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/luck-cycle | Luck Cycle (Decadal) | Decade-level overview (no Y/M/D drilling). | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/destiny-stars | Destiny Stars | Narrative for Shen Sha results. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/life-mission | Life Mission | Purpose and long-arc guidance. | regular, practitioner, corporate |
| To Do | /v1/bazi/interpretation/main-structure | Main Structure Narrative | Map 5 Structures → role archetypes. | regular, practitioner, corporate |
