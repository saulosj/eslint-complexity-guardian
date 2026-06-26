# Complexidade Ciclomática — Conceito e Referência

## O que é?

A **Complexidade Ciclomática** (Cyclomatic Complexity) é uma métrica de software proposta por Thomas McCabe
em 1976. Ela mede o número de caminhos de execução independentes em uma unidade de código (função, método).

## Como é calculada?

Cada estrutura de controle adiciona +1 ao contador:

| Estrutura | Incremento |
|---|---|
| Base (função existe) | +1 |
| `if` / `else if` | +1 cada |
| `for` / `while` / `do...while` | +1 cada |
| `case` em `switch` | +1 cada |
| `&&` / `||` em condições | +1 cada |
| `?:` (ternário) | +1 |
| `catch` | +1 |

## Exemplo prático

```javascript
// Complexidade: 1 (sem ramificações)
function somar(a, b) {
  return a + b;
}

// Complexidade: 4 (1 base + 3 if/else)
function classificar(nota) {
  if (nota >= 9) {           // +1
    return 'A';
  } else if (nota >= 7) {   // +1
    return 'B';
  } else if (nota >= 5) {   // +1
    return 'C';
  }
  return 'F';
}

// Complexidade: 6 (alta — candidata a refatoração)
function processar(usuario) {
  if (!usuario) return null;             // +1
  if (usuario.ativo && usuario.admin) { // +2 (&&)
    if (usuario.permissoes.length > 0) { // +1
      for (const perm of usuario.permissoes) { // +1
        if (perm === 'root') return true;  // +1
      }
    }
  }
  return false;
}
```

## Limites recomendados

| Limite | Significado |
|---|---|
| 1–5 | Excelente — simples e testável |
| 6–10 | Aceitável — padrão da indústria |
| 11–15 | Alto — considere refatorar |
| 16–20 | Muito alto — difícil de testar |
| 21+ | Crítico — refatoração obrigatória |

**Padrão desta Skill:** `10` (limite máximo aceitável pela indústria)

## Quando ajustar o limite?

- **Abaixar para 5–7**: projetos com alta cobertura de testes, equipes júnior, código crítico de segurança
- **Manter em 10**: maioria dos projetos web e APIs REST
- **Subir para 15**: projetos legados em migração gradual, parsers, máquinas de estado complexas

## O que acontece ao ultrapassar o limite?

Com `["error", 10]`: o ESLint **falha o build** ao encontrar uma função com complexidade > 10.
Com `["warn", 10]`: o ESLint **exibe aviso** mas não interrompe o build.

## Benefícios de controlar a complexidade

1. **Testabilidade**: funções simples exigem menos casos de teste
2. **Manutenibilidade**: código mais fácil de entender e modificar
3. **Revisão de código**: revisores identificam problemas mais rapidamente
4. **Detecção de bugs**: alta complexidade correlaciona com maior densidade de bugs
