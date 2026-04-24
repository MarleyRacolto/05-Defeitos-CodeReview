# 📦 Relatório Final

> **Atividade:** Bug Report Profissional + Code Review Guiado
> **Curso:** Qualidade de Software
> **Professor:** Prof. Claudio Nunes

---

## 👥 Identificação da dupla
# 📋 Relatório Final — Atividade 05: Defeitos & Code Review
**Dupla:** Matheus 222775 + Marley 222705
**Data:** 23/04/2026

## 📋 Sumário
- [Parte A — Bug Reports](#parte-a--bug-reports)
- [Parte B — Code Review](#parte-b--code-review)
- [Reflexão final](#-reflexão-final)
- [Declarações](#-declarações)

---

## Parte A — Bug Reports

**Dupla:** Matheus 222775 + Marley 222705
**Data da exploração:** 23/04/2026
**Navegador usado:** Chrome 121.0
**Sistema operacional:** Windows 11

---

### BUG-001

**Título:** Campo de prioridade aceita valores fora do intervalo permitido (1–5)
**Severidade:** Baixa
**Justificativa da severidade:** O defeito não impede o uso principal da aplicação — o usuário ainda consegue criar e gerenciar tarefas. Porém, dados inválidos podem causar comportamento inesperado em ordenações ou filtros futuros, comprometendo a integridade dos dados.
**Prioridade:** P4
**Justificativa da prioridade:** Trata-se de um problema de validação de entrada com baixo impacto imediato no fluxo do usuário. Pode ser corrigido em uma sprint futura sem bloquear entregas.

**Ambiente:**
- Navegador: Chrome 121.0
- Sistema Operacional: Windows 11
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Acessar a aplicação em `https://marleyracolto.github.io/05-Defeitos-CodeReview/parte-a-bug-report/app/index.html`
2. No campo "Prioridade (1-5)", digitar um valor maior que 5 (ex.: `10`) ou usar as setas do campo numérico para ultrapassar 5
3. Preencher os demais campos obrigatórios (Título, Prazo)
4. Clicar em "Adicionar tarefa"

**Resultado esperado:**
A aplicação deve rejeitar o valor e exibir uma mensagem de erro informando que a prioridade deve ser um número entre 1 e 5.

**Resultado obtido:**
A tarefa é criada normalmente com o valor de prioridade inválido (ex.: 10, 99), sem nenhum aviso ao usuário.

**Evidência:**
![Bug 001](https://github.com/user-attachments/assets/bfb75c03-ffa1-4dac-8b7a-450aee4f7a0e)

**Sugestão de causa raiz:**
O campo `<input type="number">` no HTML provavelmente não possui os atributos `min="1"` e `max="5"`, e não há validação no JavaScript antes de inserir a tarefa na lista.

---

### BUG-002

**Título:** Aplicação permite criar tarefas com título duplicado sem nenhum aviso
**Severidade:** Média
**Justificativa da severidade:** Tarefas duplicadas poluem a lista e podem confundir o usuário sobre quais itens já foram registrados, comprometendo a confiabilidade da aplicação. Não impede o uso completo do sistema, mas afeta diretamente a integridade dos dados e a experiência do usuário.
**Prioridade:** P3
**Justificativa da prioridade:** O problema ocorre em um fluxo comum (adicionar tarefa), mas não bloqueia funcionalidades críticas. Deve ser corrigido em breve para evitar degradação da usabilidade, porém não é emergencial.

**Ambiente:**
- Navegador: Chrome 121.0
- Sistema Operacional: Windows 11
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Acessar a aplicação em `https://marleyracolto.github.io/05-Defeitos-CodeReview/parte-a-bug-report/app/index.html`
2. Preencher o formulário com um título qualquer (ex.: "Estudar para a prova"), selecionar categoria, prazo e prioridade
3. Clicar em "Adicionar tarefa"
4. Sem alterar nenhum campo, clicar em "Adicionar tarefa" novamente

**Resultado esperado:**
A aplicação deve detectar que já existe uma tarefa com o mesmo título e exibir uma mensagem de aviso, impedindo ou alertando sobre a duplicação.

**Resultado obtido:**
A tarefa é adicionada uma segunda vez sem qualquer aviso, gerando duas entradas idênticas na lista. O contador "Total" incrementa normalmente como se fossem tarefas distintas.

**Evidência:**
*(Screenshot mostrando duas tarefas com o mesmo título na lista)*

**Sugestão de causa raiz:**
A função de inserção de tarefas não realiza nenhuma verificação prévia no array de tarefas para checar se já existe um item com o mesmo título antes de adicionar o novo registro.

---

### BUG-003

**Título:** Campo de prazo aceita anos arbitrários e sem sentido (ex.: ano 1, ano 9999)
**Severidade:** Média
**Justificativa da severidade:** Permitir datas absurdas compromete a integridade dos dados e pode causar comportamentos inesperados em ordenações por prazo ou cálculos de vencimento, além de passar uma impressão de falta de validação na aplicação.
**Prioridade:** P3
**Justificativa da prioridade:** Afeta a confiabilidade do dado de prazo, que é um campo central para uma lista de tarefas acadêmicas. Deve ser corrigido em breve, mas não bloqueia o fluxo principal de uso da aplicação.

**Ambiente:**
- Navegador: Chrome 121.0
- Sistema Operacional: Windows 11
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Acessar a aplicação em `https://marleyracolto.github.io/05-Defeitos-CodeReview/parte-a-bug-report/app/index.html`
2. No campo "Prazo", editar manualmente a parte do ano e digitar um valor absurdo (ex.: `0001`, `9999` ou `2500`)
3. Preencher os demais campos (Título, Categoria, Prioridade)
4. Clicar em "Adicionar tarefa"

**Resultado esperado:**
A aplicação deve validar o ano informado e rejeitar datas fora de um intervalo razoável, exibindo uma mensagem como *"Por favor, insira uma data de prazo válida."*

**Resultado obtido:**
A tarefa é criada normalmente com o ano inválido (ex.: prazo em 01/01/9999), sem nenhum aviso ou restrição, e a data absurda aparece registrada na lista de tarefas.

**Evidência:**
*(Screenshot mostrando a tarefa criada com o ano inválido visível na lista)*

**Sugestão de causa raiz:**
O campo `<input type="date">` não possui os atributos `min` e `max` definidos no HTML, e não há validação no JavaScript para verificar se o ano informado está dentro de um intervalo aceitável antes de salvar a tarefa.

---

### Matriz de Prioridade × Severidade

|              | Baixa | Média | Alta | Crítica |
|--------------|-------|-------|------|---------|
| **P1**       |       |       |      |         |
| **P2**       |       |       |      |         |
| **P3**       |       | BUG-002, BUG-003 |  |    |
| **P4**       | BUG-001 |     |      |         |

---

## Parte B — Code Review

**Arquivo revisado:** `parte-b-code-review/codigo-para-revisar.js`
**Dupla:** Matheus 222775 + Marley 222705
**Data:** 23/04/2026

### Resumo

| # | Linha | Dimensão | Rótulo | Severidade |
|---|-------|----------|--------|------------|
| 1 | 5 | Padrões | `nit` | Baixa |
| 2 | 8–44 | Erros | `major` | Média |
| 3 | 14–16 | Segurança | `blocker` | Crítica |
| 4 | 47–105 | Complexidade | `major` | Alta |
| 5 | 47–155 | Padrões | `major` | Média |
| 6 | 39 | Legibilidade | `nit` | Baixa |

---

### Findings detalhadas

#### Finding 1

**📍 Linha:** 5
**🏷 Rótulo:** `nit`
**📂 Dimensão:** Padrões

**Comentário:**
A constante `TIPOS_VALIDOS` é declarada e exportada, mas nunca utilizada
internamente para validar o campo `tipo` em `cadastrarUsuario`. Qualquer
string arbitrária pode ser salva como tipo de usuário sem nenhum bloqueio.

**Código problemático:**
```js
const TIPOS_VALIDOS = ['aluno', 'professor', 'funcionario', 'visitante'];
// nunca usada para validar dados.tipo antes de inserir
```

**Sugestão de correção:**
```js
if (!TIPOS_VALIDOS.includes(dados.tipo)) {
  throw new Error(`Tipo inválido: "${dados.tipo}". Permitidos: ${TIPOS_VALIDOS.join(', ')}`);
}
```

---

#### Finding 2

**📍 Linha:** 8–10, 19–28, 33–36, 39–44
**🏷 Rótulo:** `major`
**📂 Dimensão:** Erros

**Comentário:**
Todas as funções assíncronas do módulo realizam chamadas ao banco de dados
sem nenhum bloco `try/catch`. Se o banco falhar, a exceção se propaga sem
tratamento, podendo expor stack traces ou derrubar o processo inteiro.

Adicionalmente, na linha 40, se `db.buscarPorId` retornar `null`
(usuário inexistente), a linha seguinte `u.email = novoEmail` lança
`TypeError: Cannot set properties of null`.

**Código problemático:**
```js
async function atualizarEmail(id, novoEmail) {
  const u = await db.buscarPorId('usuarios', id); // pode retornar null
  u.email = novoEmail; // crash se u for null
  await db.atualizar('usuarios', id, u);
}
```

**Sugestão de correção:**
```js
async function atualizarEmail(id, novoEmail) {
  try {
    const usuario = await db.buscarPorId('usuarios', id);
    if (!usuario) throw new Error(`Usuário ${id} não encontrado`);
    usuario.email = novoEmail;
    await db.atualizar('usuarios', id, usuario);
    logger.info('Email atualizado: ' + novoEmail);
    return usuario;
  } catch (err) {
    logger.error('Erro ao atualizar email', err);
    throw err;
  }
}
```

---

#### Finding 3

**📍 Linha:** 14–16
**🏷 Rótulo:** `blocker`
**📂 Dimensão:** Segurança

**Comentário:**
⚠️ **Vulnerabilidade crítica — SQL Injection.** A função
`buscarUsuarioPorNome` concatena diretamente o parâmetro `nome` na
string SQL sem sanitização. Um atacante pode injetar SQL arbitrário
e comprometer todo o banco de dados.

Exemplo de ataque: passar `' OR '1'='1` retorna todos os usuários.
Payload destrutiva: `'; DROP TABLE usuarios; --`.

**Este PR não deve ser aprovado enquanto esta linha existir.**

**Código problemático:**
```js
const query = "SELECT * FROM usuarios WHERE nome = '" + nome + "'";
```

**Sugestão de correção:**
```js
async function buscarUsuarioPorNome(nome) {
  return db.executarQuery(
    'SELECT * FROM usuarios WHERE nome = ?',
    [nome]
  );
}
```

---

#### Finding 4

**📍 Linha:** 47–105
**🏷 Rótulo:** `major`
**📂 Dimensão:** Complexidade

**Comentário:**
A função `calcularLimiteEmprestimo` possui complexidade ciclomática
estimada em ~16, acima do limite recomendado de 10. O aninhamento chega
a 4 níveis de profundidade de `if/else`, tornando o código difícil de
ler, testar e manter com segurança.

**Código problemático (trecho):**
```js
if (usuario.tipo === 'professor') {
  if (usuario.tempoCasaEmDias > 365) {
    if (usuario.atrasos === 0) {
      limite = 20;
    } else {
      if (usuario.atrasos < 3) { // nível 4
```

**Sugestão de correção:**
```js
function calcularLimiteProfessor(usuario) {
  const tempoLongo = usuario.tempoCasaEmDias > 365;
  if (usuario.atrasos === 0) return tempoLongo ? 20 : 10;
  if (usuario.atrasos < 3)   return tempoLongo ? 15 : 7;
  return usuario.multaPendente ? 1 : (tempoLongo ? 3 : 2);
}

function calcularLimiteAluno(usuario) {
  if (usuario.posGraduacao) {
    if (usuario.atrasos === 0) return 10;
    if (usuario.atrasos <= 2)  return 6;
    return usuario.multaPendente ? 0 : 2;
  }
  if (usuario.bolsista)      return 6;
  return usuario.atrasos > 5 ? 1 : 4;
}

function calcularLimiteEmprestimo(usuario) {
  if (usuario.bloqueadoAte && new Date(usuario.bloqueadoAte) > new Date()) return 0;
  if (usuario.tipo === 'professor') return calcularLimiteProfessor(usuario);
  if (usuario.tipo === 'aluno')     return calcularLimiteAluno(usuario);
  return 5;
}
```

---

#### Finding 5

**📍 Linha:** 47–105 e 108–155
**🏷 Rótulo:** `major`
**📂 Dimensão:** Padrões

**Comentário:**
As funções `calcularLimiteEmprestimo` e `calcularLimiteComSuspensao`
implementam a mesma lógica de negócio para professor e aluno, com
diferenças mínimas. Qualquer mudança nas regras precisará ser replicada
em dois lugares, criando risco permanente de divergência silenciosa.

**Sugestão de correção:**
```js
function calcularLimiteEmprestimo(usuario, { verificarSuspensao = false } = {}) {
  if (verificarSuspensao && usuario.suspenso) return 0;
  if (usuario.bloqueadoAte && new Date(usuario.bloqueadoAte) > new Date()) return 0;
  if (usuario.tipo === 'professor') return calcularLimiteProfessor(usuario);
  if (usuario.tipo === 'aluno')     return calcularLimiteAluno(usuario);
  return 5;
}
```

---

#### Finding 6

**📍 Linha:** 39
**🏷 Rótulo:** `nit`
**📂 Dimensão:** Legibilidade

**Comentário:**
A variável `u` é excessivamente abreviada e não comunica que se trata
de um objeto completo de usuário recuperado do banco. Nomes de variável
devem ser autodocumentados para facilitar a leitura por qualquer membro
do time.

**Código problemático:**
```js
const u = await db.buscarPorId('usuarios', id);
u.email = novoEmail;
await db.atualizar('usuarios', id, u);
```

**Sugestão de correção:**
```js
const usuario = await db.buscarPorId('usuarios', id);
usuario.email = novoEmail;
await db.atualizar('usuarios', id, usuario);
```

---

## 💭 Reflexão final

**Qual dimensão do checklist foi mais difícil aplicar? Por quê?**

A dimensão de Complexidade foi a mais difícil de aplicar. Identificar
que a função `calcularLimiteEmprestimo` tinha complexidade ciclomática
alta exigiu percorrer mentalmente todos os caminhos possíveis do código
sem executá-lo, o que demandou atenção redobrada. Não basta ver que há
muitos `if/else` — é preciso contar os caminhos independentes e entender
o impacto real na testabilidade e manutenção do código.

**O que vocês fariam diferente se revisassem o código novamente?**

Começaríamos pela dimensão de Segurança antes de qualquer outra, pois
a vulnerabilidade de SQL Injection na linha 14 é o tipo de problema que
deve ser identificado e bloqueado imediatamente, antes mesmo de discutir
estilo ou legibilidade. Também documentaríamos cada finding já durante
a leitura fria, e não apenas na etapa final, para não perder detalhes
observados na primeira passagem pelo código.

---

## 📣 Declarações

- [x] Ambos os integrantes participaram ativamente da exploração e da revisão.
- [x] As evidências são capturas reais da aplicação em execução.
- [x] O relatório foi escrito pelos integrantes da dupla, sem cópia de terceiros.

**Matheus 222775** 

**Marley 222705** 

## 📣 Declarações


### Uso de IA como parceiro de trabalho

- [ ] Não usamos IA nesta atividade.
- [ ] Usamos IA para esclarecer conceitos teóricos.
- [ ] Usamos IA para revisar a redação dos bug reports.
- [ X] Usamos IA para discutir se um achado era ou não um defeito.
- [ ] Uso específico: [descreva]

### Declaração de autoria

Declaramos que este relatório é de autoria da dupla, que exploramos
pessoalmente a aplicação da Parte A e lemos o código da Parte B. As
findings aqui registradas representam nosso próprio julgamento
técnico.
