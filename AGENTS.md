# VSCode Copilot Agents - Central Orchestrator

## 🏛️ Agent Architecture

Arquitetura baseada em **padrão Conductor-Delegate** com 9 deidades mitológicas:
- 1 Orchestrator (Zeus) + 8 Specialized Subagents

### Orchestrator Tier

#### ⚡ **Zeus** (.github/agents/zeus.agent.md)
Central coordinator delegating work to specialized subagents.

**When to use:** Complex feature implementation, multi-layer coordination, cross-functional tasks  
**Role:** Feature orchestration, phase transition, context management  
**Delegates to:** metis → apollo → {hermes, athena, tethys} → hephaestus → tyr → mnemosyne

**Example:**
```
/implement-feature Add JWT authentication to API

Zeus orchestrates:
1. Metis plans architecture
2. Apollo explores codebase
3. Hermes implements backend
4. Athena implements frontend
5. Maat handles database migrations
6. Ra updates Docker
7. Temis reviews all changes
8. Mnemosyne documents
```

---

### Planning Tier

#### 🧠 **Metis** (.github/agents/aphrodite-subagent.agent.md)
Strategic planner with research capability. Generates detailed TDD-driven implementation roadmaps.

**When to use:** Architecture decisions, technology research, detailed planning before implementation  
**Tools:** search, usages, fetch_webpage (for external research)  
**Calls:** apollo (for parallel discovery)  
**Skills:** plan-architecture.prompt  

**Example:**
```
/plan-architecture Implement caching layer (L1 local + L2 Redis)

Metis:
1. Researches caching patterns
2. Calls Apollo for existing cache references
3. Creates detailed TDD plan
4. Proposes implementation phases
5. Hands off to Zeus for execution
```

---

### Discovery Tier

#### 🔍 **Apollo** (.github/agents/apollo-subagent.agent.md)
Parallel file discovery and intelligence gathering. Can run 3-10 simultaneous searches.

**When to use:** Rapid codebase exploration, bug root cause discovery, cross-file pattern analysis  
**Tools:** search, usages (read-only parallel searches)  
**Parallelism:** Up to 10 simultaneous search queries  
**Skills:** debug-issue.prompt  

**Example:**
```
/debug-issue NullPointerException in user service

Apollo searches (parallel):
1. "UserService" class definition
2. "NullPointer" error messages
3. User initialization code
4. Recent git commits to UserService
5. Unit tests for UserService
6. Mock data in tests

→ Synthesizes findings into root cause
```

---

### Implementation Tier (Parallel Executors)

#### 🔥 **Hermes** (.github/agents/hermes-subagent.agent.md)
Backend APIs, FastAPI services, async business logic.

**When to use:** API endpoint implementation, service layer creation, async I/O handling  
**Specialization:** FastAPI, Python, async/await, TDD backend  
**Depends on:** tethys (database), hephaestus (deployment)  
**Skills:** backend-standards.instructions, tdd-testing, api-design, security-audit  
**Tools:** search, usages, read-file, edit, runCommands  

**Backend Standards Applied:**
- Async/await on ALL I/O operations
- Type hints on all parameters
- Max 300 lines per file
- TDD first (RED → GREEN → REFACTOR)
- >80% test coverage
- Error propagation (no silent fallbacks)

---

#### 💎 **Athena** (.github/agents/aphrodite-subagent.agent.md)
Frontend UI/UX, React components, responsive design.

**When to use:** Component creation, UI improvements, accessibility fixes, state management  
**Specialization:** React, TypeScript, responsive design, WCAG accessibility  
**Depends on:** hermes (API endpoints)  
**Skills:** frontend-standards.instructions, tdd-testing, api-design  
**Tools:** search, usages, read-file, edit, runCommands  

**Frontend Standards Applied:**
- TypeScript strict mode
- Accessibility: ARIA, semantic HTML
- Responsive design (mobile-first)
- Component composition patterns
- State management discipline
- >80% test coverage (vitest)

---

#### 🌊 **Maat** (.github/agents/tethys-subagent.agent.md)
Database design, SQL optimization, migration management.

**When to use:** Schema design, query optimization, N+1 prevention, migration strategy  
**Specialization:** SQLAlchemy ORM, Alembic migrations, query analysis  
**Dependencies:** metis (planning), hermes (schema needs)  
**Skills:** database-standards.instructions, database-migration, performance-optimization, security-audit  
**Tools:** search, usages, read-file, edit, runCommands  

**Database Standards Applied:**
- Zero-downtime migration strategy
- Backward compatibility (expand-contract)
- Index strategy for performance
- N+1 query prevention
- Query plan analysis (EXPLAIN ANALYZE)
- Connection pooling configuration

---

#### ⚙️ **Ra** (.github/agents/hephaestus-subagent.agent.md)
Infrastructure, Docker containerization, deployment orchestration.

**When to use:** Container optimization, deployment strategy, infrastructure as code, CI/CD  
**Specialization:** Docker, docker-compose, multi-stage builds, health checks, CI/CD workflows  
**Depends on:** All agents (needs their deployment requirements)  
**Skills:** docker-deployment, performance-optimization  
**Tools:** search, usages, read-file, edit, runCommands  

**Infrastructure Standards Applied:**
- Multi-stage Docker builds
- Non-root user execution
- Health checks on all services
- Zero-downtime deployment strategy
- Environment variable management
- Secrets from vault (not hardcoded)

---

### Quality Assurance Tier

#### ⚖️ **Temis** (.github/agents/tyr-subagent.agent.md)
Code review, security audit, quality gates.

**When to use:** Code review before merge, security scan, test coverage validation, architecture review  
**Specialization:** Code review checklist, OWASP security audit, >80% coverage validation  
**Reviews:** All outputs from hermes, athena, tethys  
**Skills:** code-review-standards.instructions, security-audit, tdd-testing  
**Tools:** search, usages, read-file, edit, runTasks  

**Quality Gates:**
- ✅ >80% test coverage
- ✅ All OWASP Top 10 checks pass
- ✅ No hardcoded secrets
- ✅ TypeScript strict mode (frontend)
- ✅ Type hints on all functions (backend)
- ✅ Accessibility compliance (frontend)
- ✅ No SQL injection vulnerabilities
- ✅ Proper error handling

---

### Memory Tier

#### 📚 **Mnemosyne** (.github/agents/mnemosyne-subagent.agent.md)
Memory bank management, decision documentation, progress tracking.

**When to use:** End of sprint/feature, decision documentation, retrospectives, memory updates  
**Specialization:** Knowledge preservation, institutional memory, task tracking  
**Maintains:** `/docs/memory-bank/` directory structure  
**Input from:** All agents feed information  
**Skills:** None specific (documentation focused)  

**Responsibilities:**
- [ ] Update memory bank with decisions
- [ ] Document architectural patterns discovered
- [ ] Track completed features in progress log
- [ ] Archive session decisions in notes
- [ ] Maintain task index and status

---

---

## ✋ MANDATORY PAUSE POINTS

O sistema Zeus é controlado pelo usuário através de **PAUSE POINTS OBRIGATÓRIOS** em cada fase:

### Pause Point 1: Planning Approval
```
Metis cria plano detalhado
     ↓
⏸️  STOP: Usuário revisa e aprova plano
     ↓
Plano salvo em: plans/<feature-name>/plan.md
```

### Pause Point 2: Phase Implementation Review
```
Hermes/Athena/Maat implementa fase
     ↓
Temis revisa código
     ↓
⏸️  STOP: Mostrar resultado e pedir confirmação
     ↓
Resultado salvo em: plans/<feature-name>/phase-N-complete.md
```

### Pause Point 3: Git Commit
```
Zeus gera commit message
     ↓
⏸️  STOP: Usuário executa "git commit" manualmente
     ↓
Proxima fase inicia
```

**Benefício:** Você mantém controle e pode interromper em qualquer momento.

---

## 📋 Task Dispatch Patterns

### Pattern 1: Simple Bug Fix (Apollo → Hermes → Temis)
```
User: /debug-issue API returns 500 on POST /users

1. Apollo runs 3-5 parallel searches
   ├─ Extract error stack trace
   ├─ Find POST /users endpoint
   ├─ Find UserService.create()
   └─ Check error handling

2. Hermes implements fix (TDD WORKFLOW)
   ├─ Write FAILING test first
   ├─ Run test → expects FAILURE/RED
   ├─ Write minimal code to fix
   ├─ Run test → expects PASS/GREEN
   └─ Refactor and document

3. Temis reviews
   └─ Approve if coverage >80% + no OWASP issues
   
⏸️  MANDATORY STOP: User commits to git
```

### Pattern 2: Feature Implementation (Metis → Hermes/Athena/Maat → Temis → Ra)
```
User: /implement-feature Add email verification flow

1. Metis plans (triggers via /plan-architecture if needed)
   ├─ Design database schema
   ├─ Design API endpoints
   ├─ Design frontend components
   └─ Create TDD roadmap with 3-10 phases
   
⏸️  MANDATORY STOP: User approves plan
   └─ Saved: plans/email-verification/plan.md

2. For each phase (Parallel execution allowed):
   
   Phase N Implementation:
   ├─ Hermes: Write FAILING tests → minimal code → PASSING tests
   ├─ Athena: Write FAILING tests → minimal code → PASSING tests  
   └─ Maat: Write migration tests → minimal schema → passing tests
   
   Phase N Review:
   ├─ Temis validates >80% coverage + OWASP compliance
   └─ Saved: plans/email-verification/phase-N-complete.md
   
⏸️  MANDATORY STOP: User commits phase (git commit)

3. After all phases:

4. Ra updates deployment
   └─ Docker changes, env variables, health checks
   └─ Final artifact: plans/email-verification/complete.md
```

### Pattern 3: Performance Optimization (Apollo → Maat → Temis)
```
User: /optimize-database GET /products endpoint slow

1. Apollo discovers (PARALLEL SEARCHES: 3-10)
   ├─ Current ProductService.list() implementation
   ├─ Current database queries  
   ├─ Related indexes
   ├─ N+1 patterns
   └─ Cache usage
   
   ⏸️  Apollo returns structured findings, not raw code

2. Maat analyzes (CONTEXT EFFICIENT)
   ├─ Runs EXPLAIN ANALYZE
   ├─ Identifies N+1 queries
   ├─ Proposes index strategy
   ├─ Writes migration test FIRST (TDD)
   └─ Implements minimal migration code

3. Temis validates
   ├─ Benchmarks before/after
   ├─ Validates >80% test coverage
   └─ Final artifact: plans/optimize-products/complete.md
   
⏸️  MANDATORY STOP: User commits to git
```

---

## 🧠 CONTEXT WINDOW MANAGEMENT

Cada agente especializado **conserva tokens** através de estratégias:

### Apollo (Discovery)
- **Input:** Descrição do problema
- **Output:** SUMÁRIO estruturado, NÃO código raw
- **Estratégia:** Busca paralela (3-10 simultâneas) retorna apenas high-signal findings
- **Economia:** 60-70% menos tokens que raw code dump

### Hermes/Athena/Maat (Implementation)
- **Input:** Escopo de fase específica + tests a passar
- **Output:** APENAS arquivos que modifica nesta fase
- **Estratégia:** Não relê arquitetura completa, só seus arquivos
- **Economia:** 50% menos tokens vs monolithic agent

### Temis (Review)
- **Input:** Git diff (changed files only)
- **Output:** Comments estruturados com status (APPROVED/NEEDS_REVISION/FAILED)
- **Estratégia:** Revê apenas changed lines, não repositório inteiro
- **Economia:** 60% menos tokens que full codebase review

### Resultado
- **Traditional:** Single agent usa 80-90% context apenas em pesquisa/análise
- **Zeus system:** 10-15% context para análise, **70-80% livre** para reasoning profundo

---

## 🎯 TDD ENFORCEMENT WORKFLOW

Todos os agentes de implementação (Hermes, Athena, Maat) seguem **RIGOROSAMENTE**:

### Phase 1: RED (Test Fails)
```python
# Write test FIRST
def test_user_password_hashing():
    user = User(email="test@example.com", password="secret123")
    assert user.password != "secret123"  # Should be hashed
    assert user.verify_password("secret123")  # Verify works

# Run test → FAILS/RED ❌
FAILED: AssertionError: password should be hashed
```

### Phase 2: GREEN (Test Passes)
```python
# Write MINIMAL code to make test pass
class User:
    def __init__(self, email, password):
        self.email = email
        self.password = hash_password(password)  # Minimal: just hash
    
    def verify_password(self, plaintext):
        return verify_hash(plaintext, self.password)

# Run test → PASSES/GREEN ✅
PASSED: user password is hashed and verified
```

### Phase 3: REFACTOR
```python
# Improve code quality WITHOUT changing behavior
# Add validation, documentation, optimization
class User:
    """User model with secure password handling."""
    
    def __init__(self, email: str, password: str):
        if not email or not password:
            raise ValueError("Email and password required")
        self.email = email
        self.password = self._hash_password(password)
    
    @staticmethod
    def _hash_password(plaintext: str) -> str:
        """Hash password using bcrypt."""
        return bcrypt.hashpw(plaintext.encode(), bcrypt.gensalt())
    
    def verify_password(self, plaintext: str) -> bool:
        """Verify plaintext password against hash."""
        return bcrypt.checkpw(plaintext.encode(), self.password)

# Run test → STILL PASSES ✅
```

### TDD Checklist
- [ ] Write FAILING test first
- [ ] Run test, see RED/FAILED
- [ ] Write minimal code to pass
- [ ] Run test, see GREEN/PASSED
- [ ] Refactor if needed
- [ ] All tests still pass
- [ ] Coverage >80%

---

## 📁 PLAN DIRECTORY STRUCTURE

Cada feature cria um diretório documentado:

```
plans/
├── .gitignore          # Ignore plans por default
├── README.md          # Como usar plan directory
│
└── <feature-name>/
    ├── plan.md        # Plano aprovado pelo usuário
    ├── phase-1-complete.md
    ├── phase-2-complete.md
    ├── phase-3-complete.md
    └── complete.md    # Summary final
```

### plan.md (Criado por Metis, Aprovado por Usuário)
```markdown
# Feature: Email Verification Flow

**Status:** APPROVED by user on Feb 5, 2026

## Overview
Add email verification to new user registrations.

## Phases (3 total)

### Phase 1: Database Schema
- Create VerificationCode table with TTL
- Add verified_at field to User
- Tests first: validation, TTL expiry

### Phase 2: Email Service
- Create EmailService for sending
- Create VerifyEmail handler
- Tests: happy path, error handling

### Phase 3: Frontend Integration
- Create VerificationForm component
- Create ResendEmail button
- Tests: form submission, error display

## Files Affected
- Backend: models/User, models/VerificationCode, services/email.py
- Frontend: components/VerificationForm.tsx, hooks/useVerification.ts
```

### phase-N-complete.md (Criado após cada fase passar Temis review)
```markdown
# Phase 1 Complete: Database Schema

**Status:** APPROVED by Temis on Feb 5, 2026
**Coverage:** 94% (exceeds 80% requirement)

## Changes
- ✅ Created models/VerificationCode.py
- ✅ Modified models/User.py (added verified_at field)
- ✅ Created migrations/002_add_verification.py

## Tests Added
- test_verification_code_creation
- test_verification_code_expiry
- test_user_verified_at_field

## Git Commit
```
feat: Add email verification database schema

- Create VerificationCode model with 24h TTL
- Add verified_at timestamp to User
- Implement comprehensive tests (94% coverage)
```

## Decisions Made
- Used UUID for verification codes (not sequential integers)
- TTL enforced by trigger, not application logic
```

### complete.md (Summary final após todas as fases)
```markdown
# Feature Complete: Email Verification Flow

**Total Phases Completed:** 3  
**Total Coverage:** 92%  
**Total Files Modified:** 7  
**Total Time:** ~2 hours agent time  

## Phases
- ✅ Phase 1: Database Schema
- ✅ Phase 2: Email Service
- ✅ Phase 3: Frontend Integration

## Files Impacted
- models/User.py
- models/VerificationCode.py
- services/EmailService.py
- components/VerificationForm.tsx
- hooks/useVerification.ts
- migrations/002_add_verification.py
- tests/test_verification.py

## Next Steps
- [ ] Deploy to staging
- [ ] QA testing with real emails
- [ ] Deploy to production
```

---

## 🔧 Direct Invocation

Each agent can be invoked directly for bypass orchestration:

```bash
# Invoke specific agent
@hermes: Create POST /products endpoint with TDD

@tethys: Optimize users table queries

@aphrodite: Build ProductCard component with Storybook

@apollo: Find all uses of deprecated api.getUsers() method

@aphrodite: Plan migration from REST to GraphQL

@tyr: Review this PR for security issues

@hephaestus: Create multi-stage Docker build for new service

@mnemosyne: Update memory bank with completed features

@zeus: Orchestrate full feature implementation
```

---

## 🎯 Agent Selection Guide

| Need | Agent | Trigger |
|------|-------|---------|
| Plan architecture | metis | `/plan-architecture` |
| Debug issue | apollo | `/debug-issue` |
| New API endpoint | hermes | Direct: @hermes |
| New component | athena | Direct: @aphrodite |
| Database optimization | tethys | `/optimize-database` |
| Deploy changes | hephaestus | Direct: @hephaestus |
| Code review | tyr | `/review-code` |
| Document decisions | mnemosyne | Direct: @mnemosyne |
| Coordinate feature | zeus | `/implement-feature` |
| Start fresh planning | metis | `/plan-architecture` |
| Quick code search | apollo | `/debug-issue` |
| Optimize database | tethys | Direct: @tethys with EXPLAIN ANALYZE |
| Deploy to prod | hephaestus | Direct: @hephaestus with dockerfile |

---

## 🎯 MODEL FALLBACK STRATEGY

Cada agente suporta múltiplos modelos com fallback automático:

```yaml
# Zeus (Orchestrator)
model: ['Claude Sonnet 4.5 (copilot)', 'GPT-5 (copilot)']
# Prioriza a mais capaz, fallback se unavailable

# Metis (Planning)
model: ['GPT-5 (copilot)', 'Claude Sonnet 4.5 (copilot)']
# GPT-5 melhor para reasoning em planning

# Apollo (Discovery)
model: ['Gemini 3 Flash (copilot)', 'Claude Haiku 4.5 (copilot)']
# Flash é rápido para buscas paralelas

# Hermes/Athena/Maat (Implementation)
model: ['Claude Sonnet 4.5 (copilot)', 'Claude Haiku 4.5 (copilot)']
# Sonnet para complexidade, fallback para Haiku (economico)

# Temis (Review)
model: ['Claude Sonnet 4.5 (copilot)', 'GPT-5 (copilot)']
# Requer reasoning profundo para code review

# Mnemosyne (Memory)
model: ['Claude Haiku 4.5 (copilot)']  
# Haiku é suficiente para documentação
```

**Benefício:** Se modelo principal estiver unavailable, sistema usa fallback automaticamente.

---

## 🔧 CUSTOM AGENT EXTENSION

Para criar um novo agente especializado (exemplo: Database-Expert):

### Step 1: Create Agent File
```bash
mkdir -p .github/agents
cat > .github/agents/database-expert-subagent.agent.md << 'EOF'
---
name: database-expert
user-invokable: false  # Only for internal delegation
description: Specialized database architect and query optimizer
argument-hint: "Analyze and optimize database schema and queries"
model: ['Claude Sonnet 4.5 (copilot)', 'GPT-5 (copilot)']
tools: ['search', 'usages', 'edit', 'runCommands']
---

You are a DATABASE EXPERT SUBAGENT.

**Your specialty:** SQL optimization, schema design, perf tuning
**Your scope:** Database layer changes, migrations, index strategy

**Core workflow:**
1. Analyze current database structure
2. Identify bottlenecks with EXPLAIN ANALYZE
3. Propose schema or index optimizations
4. Write migration tests FIRST (TDD)
5. Implement minimal schema changes
6. Return structured findings

[Add your detailed instructions]
EOF
```

### Step 2: Register with Zeus
Edit `.github/agents/zeus.agent.md` and add:
```markdown
**10. DatabaseExpert-subagent**: Especialista em SQL e schema design
- Use para análises de query performance
- Invoque para designs de schema complexos
- Sempre retorna structured findings, nunca raw SQL dumps
```

### Step 3: Register with Metis (for planning phase)
Edit `.github/agents/aphrodite-subagent.agent.md` and add:
```markdown
**When researching database architecture, delegate to DatabaseExpert-subagent:**
- Goal: Analyze current schema and identify optimization opportunities
- Instructions: Use EXPLAIN ANALYZE, check indexes, find N+1 patterns
- Return: Structured findings with specific recommendations
```

### Step 4: Test Integration
```bash
# Invoke directly
@database-expert: Analyze the users table queries for N+1 problems

# Or through Zeus
@zeus: Use database-expert to optimize the product search queries
```

### Custom Agent Checklist
- [ ] Create `.agent.md` file with proper frontmatter
- [ ] Set `user-invokable: false` if internal only
- [ ] Define tools needed (search, edit, runCommands, etc)
- [ ] Add single responsibility focus
- [ ] Document in Zeus agents list
- [ ] Document in relevant Planning/Implementation agents
- [ ] Test with sample task
- [ ] Add to memory bank if discovering new patterns

---

## � ARTIFACTS GENERATED BY WORKFLOW

Cada execução do Zeus cria artifacts documentados:

### Durante Planning Phase
```
plans/<feature-name>/
└── plan.md              (Estrutura completa, 3-10 fases, TDD roadmap)
```
**Contém:**
- Feature overview and objectives
- Fase-by-fase breakdown com test requirements
- Listed files to create/modify
- Open questions for user
- Risk assessment

### Durante Implementation Phase (por phase)
```
plans/<feature-name>/
└── phase-N-complete.md  (Resultado de CADA fase após Temis approval)
```
**Contém:**
- Phase objective e summary
- Files created/modified
- Tests created/passed
- Coverage percentage
- Temis review result (APPROVED/NEEDS_REVISION/FAILED)
- Git commit message
- Decisions made in this phase

### Após Completion
```
plans/<feature-name>/
└── complete.md          (Summary final de todo projeto)
```
**Contém:**
- Total phases completed checklist
- Total coverage percentage
- Complete file impact list
- Key functions/classes added
- Test coverage summary
- Recommendations for next steps

### Benefits da Artifact Trail
- ✅ **Audit Trail**: Review exato do que foi feito
- ✅ **Knowledge Transfer**: Novos team members entendem decisões
- ✅ **Project Documentation**: Natural documentation do feature dev
- ✅ **PR Descriptions**: Copie plan.md para seu PR
- ✅ **Resumable Work**: Se interrompido, continue de qualquer phase

---

## �📚 References

- **Agent Skills:** `.github/skills/*/SKILL.md`
- **Custom Instructions:** `.github/instructions/*-standards.instructions.md`
- **Prompt Files:** `.github/prompts/*.prompt.md`
- **Agent Definitions:** `.github/agents/*.agent.md`
- **Memory Bank:** `/docs/memory-bank/`
- **VSCode Settings:** `.vscode/settings.json`

---

**Last Updated:** [AUTO-UPDATED on agent creation]  
**Total Agents:** 9 (1 orchestrator + 8 specialized)  
**Total Skills:** 6  
**Total Custom Instructions:** 5  
**Total Prompt Files:** 5  
**Architecture Pattern:** Conductor-Delegate  
**Mythology Reference:** Greek, Norse, Egyptian Deities
