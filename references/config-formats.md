# Formatos de Configuração ESLint — Guia de Edição

## 1. `.eslintrc.json` (JSON puro)

Formato mais comum. Edite o objeto `rules`:

```json
{
  "extends": ["eslint:recommended"],
  "rules": {
    "no-console": "warn",
    "complexity": ["error", 10]
  }
}
```

**Atenção:** JSON não aceita trailing comma nem comentários.

---

## 2. `.eslintrc.js` ou `.eslintrc.cjs` (CommonJS)

```javascript
module.exports = {
  extends: ['eslint:recommended'],
  rules: {
    'no-console': 'warn',
    'complexity': ['error', 10],
  },
};
```

**Vantagem:** Aceita comentários e lógica condicional.

---

## 3. `.eslintrc.yaml` / `.eslintrc.yml` (YAML)

```yaml
extends:
  - eslint:recommended
rules:
  no-console: warn
  complexity:
    - error
    - 10
```

**Atenção:** Indentação com espaços (não tabs). A regra `complexity` vira uma lista YAML.

---

## 4. `eslint.config.js` — Flat Config (ESLint v9+)

Este é o formato moderno. A estrutura é diferente:

```javascript
import js from '@eslint/js';

export default [
  js.configs.recommended,
  {
    rules: {
      'no-console': 'warn',
      'complexity': ['error', 10],
    },
  },
];
```

**Como identificar:** O arquivo usa `export default` (ESM) e não tem campo `extends` no estilo antigo.

**Variante `.mjs`:** Idêntica, apenas a extensão muda.

---

## 5. `package.json` → campo `"eslintConfig"`

```json
{
  "name": "meu-projeto",
  "eslintConfig": {
    "extends": ["react-app"],
    "rules": {
      "complexity": ["error", 10]
    }
  }
}
```

**Atenção:** Edite APENAS o campo `eslintConfig`. Não toque em `scripts`, `dependencies`, etc.

---

## Regra `complexity` em presets populares

Alguns presets já definem a regra. Nesses casos, **sobrescreva no campo `rules`** local:

| Preset | Define `complexity`? | Valor padrão |
|---|---|---|
| `eslint:recommended` | ❌ Não | — |
| `airbnb` | ✅ Sim | `["error", 20]` |
| `standard` | ❌ Não | — |
| `google` | ❌ Não | — |
| `xo` | ✅ Sim | `["error", 20]` |

Para sobrescrever um preset:

```json
{
  "extends": ["airbnb"],
  "rules": {
    "complexity": ["error", 10]
  }
}
```

A regra local tem prioridade sobre o preset.

---

## Verificando a versão do ESLint

Para saber qual formato usar:

```bash
npx eslint --version
```

- **v8 ou inferior** → Use `.eslintrc.*`
- **v9+** → Use `eslint.config.js` (Flat Config) ou `.eslintrc.*` em modo de compatibilidade

---

## Validando a configuração após a edição

```bash
# Verificar se a configuração é válida
npx eslint --print-config src/index.js

# Testar a regra em um arquivo específico
npx eslint src/algum-arquivo.js --rule '{"complexity": ["error", 10]}'
```
