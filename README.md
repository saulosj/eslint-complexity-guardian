# 🛡️ ESLint Complexity Guardian

> Uma Skill para Claude que configura **cirurgicamente** a regra de Complexidade Ciclomática no ESLint, sem modificar nenhuma outra parte do projeto.

---

## O que esta Skill faz

Quando ativada, o Claude age como um especialista focado exclusivamente em:

1. Localizar o arquivo de configuração ESLint do projeto
2. Verificar se a regra `complexity` já existe
3. Adicionar ou atualizar **apenas** essa regra
4. Exibir um diff claro das alterações
5. Explicar o impacto da mudança

**Nada mais é tocado.** Nenhum outro arquivo, regra, dependência ou configuração.

---

## Instalação

### Opção 1 — Arquivo `.skill` (recomendado)

1. Baixe o arquivo `eslint-complexity-guardian.skill`
2. No Claude.ai, acesse **Settings → Skills**
3. Clique em **Install Skill** e selecione o arquivo

### Opção 2 — Manual

Copie a pasta `eslint-complexity-guardian/` para o diretório de skills do Claude:

```
~/.claude/skills/eslint-complexity-guardian/
├── SKILL.md
└── references/
    ├── complexity-explained.md
    └── config-formats.md
```

---

## Como usar

Simplesmente peça ao Claude em linguagem natural:

```
"Adicione a regra de complexity ao ESLint com limite 10"
"Configure o ESLint Complexity Guardian no meu projeto"
"Quero limitar a complexidade ciclomática a 8 no ESLint"
"Ajuste a regra complexity para warn com limite 15"
```

---

## Formatos de configuração suportados

| Arquivo | Formato |
|---|---|
| `.eslintrc.json` | JSON |
| `.eslintrc.js` / `.eslintrc.cjs` | CommonJS |
| `.eslintrc.yaml` / `.eslintrc.yml` | YAML |
| `eslint.config.js` / `eslint.config.mjs` | Flat Config (ESLint v9+) |
| `package.json` → `"eslintConfig"` | JSON embutido |

---

## Exemplo de saída

```
📁 Arquivo encontrado: .eslintrc.json

📋 Configuração anterior:
{
  "extends": ["eslint:recommended"],
  "rules": {
    "no-console": "warn"
  }
}

✅ Configuração nova:
{
  "extends": ["eslint:recommended"],
  "rules": {
    "no-console": "warn",
    "complexity": ["error", 10]
  }
}

📝 Diff:
  "rules": {
    "no-console": "warn",
+   "complexity": ["error", 10]
  }

💡 Impacto:
A regra complexity["error", 10] fará o ESLint falhar o build sempre que uma função
ultrapassar 10 caminhos de execução independentes. Isso incentiva funções menores,
mais testáveis e fáceis de manter. O limite 10 é o padrão recomendado pela indústria.

✅ Confirmação: Nenhuma outra parte do projeto foi modificada.
```

---

## Checklist de validação

Antes de finalizar, a Skill valida automaticamente:

- ✅ Apenas a regra `complexity` foi alterada
- ✅ Nenhum código de negócio foi modificado
- ✅ Nenhuma dependência foi instalada
- ✅ A configuração ESLint continua válida
- ✅ O projeto permanece compatível

---

## Parte de uma família de Skills

Esta Skill é a primeira de uma biblioteca de **Engineering Guardians**:

| Skill | Status |
|---|---|
| 🛡️ **ESLint Complexity Guardian** | ✅ Disponível |
| 💅 Prettier Guardian | 🔜 Em breve |
| 🔷 TypeScript Guardian | 🔜 Em breve |
| 🔒 Security Guardian | 🔜 Em breve |
| ⚡ Performance Guardian | 🔜 Em breve |
| ⚛️ React Guardian | 🔜 Em breve |
| 🌐 Next.js Guardian | 🔜 Em breve |
| 🟢 Node Guardian | 🔜 Em breve |

---

## Estrutura da Skill

```
eslint-complexity-guardian/
├── SKILL.md                          # Instruções principais + fluxo de trabalho
└── references/
    ├── complexity-explained.md       # Conceito, exemplos, limites recomendados
    └── config-formats.md             # Como editar cada formato ESLint
```

---

## Licença

MIT — Livre para usar, modificar e distribuir.

---

*Criado com [Claude Skills](https://claude.ai) · Parte do projeto [Nexus Engineering](https://nexusvc.app)*
