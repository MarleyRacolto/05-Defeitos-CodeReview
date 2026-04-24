# 🔎 Formulário — Parte B

> Preencha uma seção por finding. O mínimo esperado é **6 findings**.

**Dupla:** [Matheus 222775 + [Marley 222705
**Data da revisão:** 23/04/2026
---

### Finding #1

**📍 Linha(s):*5*
**🏷 Rótulo:**  nit 
**📂 Dimensão:** PADRAO
**⚠️ Severidade:** PADORES

**🐛 Problema:*A  constante TIPOS_VALIDOS é declarada e exportada, mas nunca utilizada*

**💡 Sugestão de correção:*async function cadastrarUsuario(dados) {
  if (!TIPOS_VALIDOS.includes(dados.tipo)) {
    throw new Error(`Tipo inválido: ${dados.tipo}`);
  }
  // ...restante do código
}*



**📚 Referência (opcional):**

---

### Finding #2

**📍 Linha(s):*0–12 / 33–36 / 39–43*
**🏷 Rótulo:*major*
**📂 Dimensão:*ALTA*
**⚠️ Severidade:*LEGIBILIDADE *

**🐛 Problema:*As funções listarUsuariosAtivos, buscarUsuarioPorNome, cadastrarUsuario e atualizarEmail fazem chamadas assíncronas ao banco (db.executarQuery, db.insert, db.buscarPorId, db.atualizar) sem nenhum bloco try/catch. Se o banco falhar, a exceção vai se propagar sem tratamento, podendo derrubar a aplicação ou expor stack traces ao cliente.*

**💡 Sugestão de correção:*// Linha 10 — sem try/catch
async function listarUsuariosAtivos() {
  return db.executarQuery('SELECT * FROM usuarios WHERE ativo = 1');
}

// Linha 39 — sem try/catch
async function atualizarEmail(id, novoEmail) {
  const u = await db.buscarPorId('usuarios', id);
  // se id não existir, u é null e a linha seguinte quebra
  u.email = novoEmail;*

```javascript
// ajuste sugerido
```

---

---


**⚠️ Severidade:**

**🐛 Problema:**

**💡 Sugestão de correção:**

```javascript
// ajuste sugerido
```

---

### Finding #4

**📍 Linha(s):*47–105*
**🏷 Rótulo:*major*
**📂 Dimensão:*ALTA*
**⚠️ Severidade:ERROS*

**🐛 Problema:*A função calcularLimiteEmprestimo possui complexidade ciclomática muito acima de 10 (estimada em ~16 caminhos independentes), com if/else aninhados em até 4 níveis de profundidade. Isso torna o código extremamente difícil de testar, manter e entender.*

**💡 Sugestão de correção:*function calcularLimiteProfessor(usuario) { ... }
function calcularLimiteAluno(usuario) { ... }

function calcularLimiteEmprestimo(usuario) {
  if (usuario.bloqueadoAte && new Date(usuario.bloqueadoAte) > new Date()) return 0;
  if (usuario.tipo === 'professor') return calcularLimiteProfessor(usuario);
  if (usuario.tipo === 'aluno') return calcularLimiteAluno(usuario);
  return 5;
}*

```javascript
// ajuste sugerido
```

---

### Finding #5

**📍 Linha(s):*47–105 vs. 108–155*
**🏷 Rótulo:*MAJOR*
**📂 Dimensão:*ALTA*
**⚠️ Severidade:*SEGURANCA*

**🐛 Problema:*As funções calcularLimiteEmprestimo (linha 47) e calcularLimiteComSuspensao (linha 108) implementam a mesma lógica de cálculo de limite por tipo de usuário, com diferenças mínimas (a segunda trata suspenso explicitamente e usa else if em vez de if aninhados). Qualquer alteração nas regras de negócio precisará ser replicada em dois lugares, gerando risco de divergência.*

**💡 Sugestão de correção:*function calcularLimiteEmprestimo(usuario, { verificarSuspensao = false } = {}) {
  if (verificarSuspensao && usuario.suspenso) return 0;
  // ...lógica unificada
}*

```javascript
// ajuste sugerido
```

---

### Finding #6

**📍 Linha(s):*39 / 47*
**🏷 Rótulo:*nit*
**📂 Dimensão:*PADRAO
**⚠️ Severidade:**BAIXA 

**🐛 Problema:*A variável u na função atualizarEmail (linha 39) e o parâmetro implícito de loop interno são nomes extremamente pouco descritivos. u não comunica que se trata de um objeto de usuário completo, dificultando a leitura por qualquer outra pessoa que revise o código.*

**💡 Sugestão de correção:*async function atualizarEmail(id, novoEmail) {
  const usuario = await db.buscarPorId('usuarios', id);
  usuario.email = novoEmail;
  await db.atualizar('usuarios', id, usuario);*



## ✅ Checklist final

- [ ✅ ] Há pelo menos 6 findings preenchidas
- [ ✅ ] Cada finding cita linha, dimensão, rótulo e severidade
- [ ✅ ] As sugestões são concretas e acionáveis
- [ ✅ ] Pelo menos uma finding cobre segurança
- [ ✅ ] Pelo menos uma finding cobre complexidade
