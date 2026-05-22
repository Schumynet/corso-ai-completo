# MODULO AI-5: OPENHANDS

## Lezione AI-5.1: Introduzione a OpenHands

### Cos'è OpenHands?

**OpenHands** è una piattaforma open-source per creare AI agents che possono:
- Usare strumenti (bash, browser, API)
- Automatizzare workflow complessi
- Interagire con sistemi esterni
- Lavorare in modo autonomo

### Confronto con Altri Framework

| Feature | OpenHands | LangChain | AutoGPT |
|---------|-----------|-----------|---------|
| Open Source | ✅ | ✅ | ✅ |
| Browser Automation | ✅ | ❌ | ❌ |
| Code Agents | ✅ | ✅ | ✅ |
| Cloud Hosting | ✅ | ❌ | ❌ |
| Automation Jobs | ✅ | ❌ | ❌ |
| Skill System | ✅ | ❌ | ❌ |

### Architettura OpenHands

```
┌─────────────────────────────────────────────────────────┐
│                    OPENHANDS                              │
│                                                          │
│  ┌─────────────────────────────────────────────────┐    │
│  │              AGENT (LLM + Tools)                  │    │
│  │                                                   │    │
│  │   ┌─────────┐  ┌─────────┐  ┌─────────┐       │    │
│  │   │ Terminal │  │ Browser │  │  File   │       │    │
│  │   │  Tool   │  │  Tool   │  │  Tool   │       │    │
│  │   └─────────┘  └─────────┘  └─────────┘       │    │
│  │                                                   │    │
│  │   ┌─────────┐  ┌─────────┐  ┌─────────┐       │    │
│  │   │   API   │  │  Git    │  │ Custom  │       │    │
│  │   │  Tool   │  │  Tool   │  │  Tool   │       │    │
│  │   └─────────┘  └─────────┘  └─────────┘       │    │
│  └─────────────────────────────────────────────────┘    │
│                    ↓                                       │
│  ┌─────────────────────────────────────────────────┐    │
│  │              AUTOMATION LAYER                      │    │
│  │                                                   │    │
│  │   ┌─────────────┐  ┌─────────────┐               │    │
│  │   │ Cron Jobs   │  │  Webhooks  │               │    │
│  │   └─────────────┘  └─────────────┘               │    │
│  │                                                   │    │
│  │   ┌─────────────────────────────────┐             │    │
│  │   │        Skill System              │             │    │
│  │   └─────────────────────────────────┘             │    │
│  └─────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
```

### Componenti Principali

#### 1. Agent
Il nucleo che processa richieste e usa tools:
```python
# Concetto base
agent = Agent(
    model="gpt-4",
    tools=[terminal, browser, file_editor],
    system_prompt="Sei un assistant che può usare vari strumenti"
)
```

#### 2. Tools
Strumenti predefiniti per interagire con il mondo:
- **Terminal**: Esegue comandi bash
- **Browser**: Naviga web, compila form
- **FileEditor**: Legge, scrive, modifica file
- **BrowserGetContent**: Estrae contenuto da pagine

#### 3. Skills
Estensioni che aggiungono capacità specifiche:
```python
skill = Skill(
    name="github",
    description="Interagisci con GitHub",
    triggers=["github", "repository", "pull request"],
    source="github:OpenHands/extensions/skills/github"
)
```

### Modalità di Utilizzo

#### 1. GUI (Graphical User Interface)
Interfaccia web per conversare con l'agent:
- Accesso da browser
- Visibilità in tempo reale delle azioni
- Storia delle conversazioni

#### 2. CLI (Command Line Interface)
Uso da terminale:
```bash
openhands --task "Crea un file README.md"
```

#### 3. API / Cloud
Deploy come servizio:
```python
# OpenHands Cloud API
response = requests.post(
    "https://api.openhands.ai/v1/agent/run",
    headers={"Authorization": f"Bearer {API_KEY}"},
    json={
        "task": "Crea un report settimanale",
        "tools": ["browser", "terminal"],
        "skills": ["github"]
    }
)
```

### Quick Start

```python
from openhands.agent import Agent

# Crea un agent
agent = Agent(
    model="anthropic/claude-3-sonnet",
    tools=["terminal", "file_editor", "browser"],
    system_prompt="Sei un developer assistant. Puoi scrivere codice, eseguire comandi, navigare il web."
)

# Esegui un task
result = agent.run("Crea un progetto Python chiamato 'mio_progetto'")

print(result)
```

### Quando Usare OpenHands

✅ **Ideale per:**
- Automatizzare task di sviluppo
- Code review automatizzato
- Data entry e web scraping
- Report generation
- DevOps automation

❌ **Non ideale per:**
- Task che richiedono output in tempo reale (< 1s)
- Interfacce grafiche complesse non accessibili via browser
- Sistemi che richiedono autenticazione forte non supportata

### Esercizio

1. Vai su https://app.all-hands.dev
2. Crea un account o effettua login
3. Fai una semplice richiesta all'agent (es. "Ciao, puoi aiutarmi?")
4. Prova a chiedere qualcosa di concreto (es. "Crea un file di testo")

---

## Lezione AI-5.2: Automations con OpenHands

### Cosa sono le Automations?

Le **Automations** sono agent pre-configurati che girano automaticamente:
- Su schedule (cron)
- In risposta a eventi (webhooks)

### Trigger Types

```
┌─────────────────────────────────────────────────────────┐
│                  AUTOMATION TRIGGERS                     │
│                                                          │
│  ┌─────────────────────┐  ┌─────────────────────┐       │
│  │    CRON TRIGGER    │  │   EVENT TRIGGER    │       │
│  │                     │  │                     │       │
│  │  ┌───────────────┐ │  │  ┌───────────────┐ │       │
│  │  │ 0 9 * * *     │ │  │  │  GitHub PR    │ │       │
│  │  │ (ogni giorno  │ │  │  │  opened       │ │       │
│  │  │  alle 9:00)   │ │  │  └───────────────┘ │       │
│  │  └───────────────┘ │  │                     │       │
│  │                     │  │  ┌───────────────┐ │       │
│  │  ┌───────────────┐ │  │  │  Stripe       │ │       │
│  │  │ */15 * * * *  │ │  │  │  payment      │ │       │
│  │  │ (ogni 15 min) │ │  │  └───────────────┘ │       │
│  │  └───────────────┘ │  │                     │       │
│  └─────────────────────┘  └─────────────────────┘       │
└─────────────────────────────────────────────────────────┘
```

### Cron Expressions

```python
# Formato: minuto ora giorno_del_mese mese giorno_della_settimana

# Esempi:
"0 9 * * *"        # Ogni giorno alle 9:00
"0 9 * * 1-5"      # Lun-Ven alle 9:00
"*/15 * * * *"      # Ogni 15 minuti
"0 0 1 * *"        # Primo del mese a mezzanotte
"0 */6 * * *"      # Ogni 6 ore
"30 18 * * 0"      # Ogni domenica alle 18:30
```

### Creare un'Automation via API

```python
import requests

OPENHANDS_API = "https://app.all-hands.dev"
API_KEY = "your-api-key"

# 1. Crea automation con Prompt Preset
automation = requests.post(
    f"{OPENHANDS_API}/api/automation/v1/preset/prompt",
    headers={
        "Authorization": f"Bearer {API_KEY}",
        "Content-Type": "application/json"
    },
    json={
        "name": "Daily GitHub Summary",
        "prompt": "Genera un riepilogo quotidiano delle attività GitHub e invialo via email.",
        "trigger": {
            "type": "cron",
            "schedule": "0 9 * * *",
            "timezone": "Europe/Rome"
        },
        "timeout": 300
    }
)

print(automation.json())
```

### Automazioni Comuni

#### 1. Code Review Automatico

```python
# Trigger: PR aperto su GitHub
automation = {
    "name": "Auto Code Review",
    "prompt": """
    Analizza questo Pull Request per:
    1. Qualità del codice
    2. Potenziali bug
    3. Security issues
    4. Best practices mancate
    
    Fornisci feedback costruttivo in italiano.
    """,
    "trigger": {
        "type": "event",
        "source": "github",
        "on": "pull_request.opened"
    }
}
```

#### 2. Issue Triage

```python
automation = {
    "name": "Issue Triage",
    "prompt": """
    Analizza questo issue e:
    1. Suggerisci labels appropriate
    2. Identifica se è bug, feature o question
    3. Valuta la priorità (low/medium/high/critical)
    4. Se mancano informazioni, chiedile gentilmente
    
    Rispondi in italiano.
    """,
    "trigger": {
        "type": "event",
        "source": "github",
        "on": "issues.opened"
    }
}
```

#### 3. Weekly Report

```python
automation = {
    "name": "Weekly Report",
    "prompt": """
    Genera un report settimanale che include:
    1. Riepilogo delle attività della settimana
    2. Metriche principali (se disponibili)
    3. Issues aperti/chiusi
    4. Prossimi passi
    
    Formatta in Markdown e invia a email配置ata.
    """,
    "trigger": {
        "type": "cron",
        "schedule": "0 18 * * 5",  # Venerdì alle 18:00
        "timezone": "Europe/Rome"
    }
}
```

### Workflow Examples

#### Web Scraping Automation

```python
automation = {
    "name": "Monitoraggio Prezzi",
    "prompt": """
    Esegui le seguenti operazioni:
    1. Vai su [sitoweb] e cerca il prodotto specificato
    2. Estrai prezzo attuale e disponibilità
    3. Confronta con il prezzo precedente (leggi da file prezzi.json)
    4. Se il prezzo è calato > 10%, invia notifica email
    5. Aggiorna prezzi.json con il nuovo prezzo
    
    Prodotti da monitorare: [lista]
    """,
    "trigger": {
        "type": "cron",
        "schedule": "0 8 * * *",  # Ogni giorno alle 8:00
        "timezone": "Europe/Rome"
    }
}
```

### Monitoring e Logs

```python
# Lista le automation
automations = requests.get(
    f"{OPENHANDS_API}/api/automation/v1",
    headers={"Authorization": f"Bearer {API_KEY}"}
)

# Lista le run di un'automation
runs = requests.get(
    f"{OPENHANDS_API}/api/automation/v1/{automation_id}/runs",
    headers={"Authorization": f"Bearer {API_KEY}"}
)

# Dispatch manuale
requests.post(
    f"{OPENHANDS_API}/api/automation/v1/{automation_id}/dispatch",
    headers={"Authorization": f"Bearer {API_KEY}"}
)
```

### Best Practices

```python
# ✅ Usa timeout appropriati
timeout = 300  # 5 minuti per task semplici
timeout = 1800  # 30 minuti per task complessi

# ✅ Includi error handling nel prompt
prompt = """
Esegui il task. Se incontri errori:
1. Riprova fino a 3 volte
2. Se fallisce, invia notifica con errore
3. Logga tutto per debugging
"""

# ✅ Usa repo cloning per contesto
json={
    "repos": [
        {"url": "owner/repo", "ref": "main"}
    ]
}
```

### Esercizio

1. Crea un'automation che risponde automaticamente a issue GitHub con label "question"
2. Crea un'automation che ogni mattina alle 8:00 fa un backup di un file importante
3. Testa l'automation con dispatch manuale

---

## Lezione AI-5.3: Skills e Integrazioni

### Il Sistema di Skills

Le **Skills** sono estensioni che aggiungono capacità specifiche all'agent:

```
┌─────────────────────────────────────────────────────────┐
│                    SKILL ECOSYSTEM                       │
│                                                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │   GitHub    │  │   GitLab    │  │  Bitbucket  │     │
│  │   Skill     │  │   Skill     │  │   Skill     │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
│                                                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │    Linear   │  │  Discord    │  │  Notion    │     │
│  │   Skill     │  │   Skill     │  │   Skill    │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
│                                                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │    Jira     │  │    Slack    │  │  Custom    │     │
│  │   Skill     │  │   Skill     │  │   Skill    │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────┘
```

### Skills Popolari

#### GitHub Skill
```python
# Capacità:
# - Creare issue e PR
# - Commentare su PR
# - Gestire labels
# - Fare code review

# Trigger keywords: "github", "repository", "pull request", "issue"
```

#### GitLab Skill
```python
# Capacità:
# - Gestire merge request
# - Creare snippet
# - Interagire con wiki

# Trigger: "gitlab", "merge request"
```

#### Linear Skill
```python
# Capacità:
# - Creare e aggiornare issue
# - Gestire cicli di sprint
# - Assignee management

# Trigger: "linear", "issue", "sprint"
```

### Usare Skills nelle Automations

```python
# Con Plugin Preset
automation = requests.post(
    f"{OPENHANDS_API}/api/automation/v1/preset/plugin",
    headers={
        "Authorization": f"Bearer {API_KEY}",
        "Content-Type": "application/json"
    },
    json={
        "name": "GitHub Issue Triage",
        "plugins": [
            {"source": "github:OpenHands/extensions/skills/github"}
        ],
        "prompt": """
        Quando arriva un nuovo issue GitHub:
        1. Analizza il contenuto
        2. Suggerisci labels appropriate
        3. Se è un bug, chiedi passi per riprodurlo
        4. Assegna a persona appropriata se possibile
        """,
        "trigger": {
            "type": "event",
            "source": "github",
            "on": "issues.opened"
        }
    }
)
```

### Creare una Skill Personalizzata

```python
# Struttura di una skill
"""
my-custom-skill/
├── SKILL.md          # Definizione e istruzioni
├── references/       # Documentazione di riferimento
│   └── guide.md
└── assets/          # Risorse (opzionali)
    └── logo.png
"""

# SKILL.md example
"""
# My Custom Skill

TRIGGER: ["custom", "mio comando"]

CAPACITIES:
- Esegui operazione X
- Genera report Y
- Invia notifica Z

USAGE:
Quando l'utente dice qualcosa che matchaa i trigger,
usa questa skill per completare il task.
"""
```

### Integrazioni API

```python
# Creare un'integrazione custom
integration = {
    "name": "My CRM",
    "api_base": "https://api.my-crm.com",
    "auth": "api_key",  # o "oauth2", "bearer"
    "endpoints": {
        "contacts": "/contacts",
        "deals": "/deals",
        "tasks": "/tasks"
    }
}
```

### Webhook Integrations

```python
# Stripe
{
    "trigger": "charge.succeeded",
    "action": "Aggiorna Dashboard con nuovo pagamento",
    "filter": "amount > 100"
}

# Slack
{
    "trigger": "message.posted",
    "action": "Analizza messaggio e se contiene 'urgent', crea issue",
    "filter": "channel == '#support'"
}
```

### Skill Composition

```python
# Combina più skills in un'automation
automation = {
    "name": "Full Stack Dev Agent",
    "plugins": [
        {"source": "github:OpenHands/extensions/skills/github"},
        {"source": "linear:OpenHands/extensions/skills/linear"},
        {"source": "discord:OpenHands/extensions/skills/discord"}
    ],
    "prompt": """
    Sei un full-stack developer assistant.
    
    Puoi:
    - Creare/modificare codice su GitHub
    - Gestire issue e sprint su Linear
    - Comunicare aggiornamenti su Discord
    
    Quando ti viene chiesto di implementare una feature:
    1. Crea branch su GitHub
    2. Implementa il codice
    3. Crea PR con descrizione completa
    4. Aggiungi task su Linear per review
    5. Notifica il team su Discord
    """
}
```

### Esercizio Finale

1. Esplora il repository OpenHands extensions su GitHub
2. Identifica 3 skills utili per il tuo workflow
3. Crea un'automation che usa almeno 2 skills insieme

---

## Riepilogo Modulo AI-5

### Concetti Chiave
- OpenHands è una piattaforma per AI agents e automazione
- Automations possono essere triggerate da cron o eventi
- Skills estendono le capacità con integrazioni specifiche
- Il sistema supporta deployment cloud e self-hosted

### Prossimi Passi
- Esplora la documentazione su docs.openhands.dev
- Prova a creare la tua prima automation
- Unisciti alla community su GitHub Discussions