# 🐛 Bug Reports — Parte A

> Preencha uma seção completa para cada defeito encontrado. O mínimo
> exigido é **3 bug reports**. Apague este bloco antes de entregar.

**Dupla:** [Matheus 222775] + [Marley 222705]
**Data da exploração:** [23/04/2026]
**Navegador usado:** [Chrome 121 / Firefox 122 / Safari 17 / …]
**Sistema operacional:** [Windows 11 / macOS 14 / Ubuntu 22.04 / …]

---

## BUG-001

**Título:*Salvar tarefa sem titulo * 
**Severidade:** Crítica 
**Justificativa da severidade:*O título é o campo principal e identificador de uma tarefa. Permitir salvar sem ele gera registros sem sentido na lista, impossibilitando que o usuário saiba o que deve ser feito, o que quebra a funcionalidade central da aplicação.* 
**Prioridade:** P1 
**Justificativa da prioridade:* Uma tarefa sem título é completamente inútil e não deveria existir no sistema. Por tratar-se do campo mais essencial da aplicação, a ausência de validação nesse ponto deve ser corrigida imediatamente, antes de qualquer outra entrega.* 
**Ambiente:**
- Navegador: [ex.: Chrome 121.0]
- Sistema Operacional: [ex.: Windows 11]
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1-Deixar o campo "Título" completamente em branco
2-Preencher os demais campos (Categoria, Prazo e Prioridade) normalmente
3-Clicar em "Adicionar tarefa

**Resultado esperado:**
Atividades com titulos unicos 

**Resultado obtido:**
Atividade sem titulo 

**Evidência:**
<img width="763" height="681" alt="image" src="https://github.com/user-attachments/assets/be23d8d0-4610-48cf-8cbb-8fb5da5afc77" />




**Sugestão de causa raiz (opcional):**
[Palpite informado — útil para quem vai corrigir.]

---

## BUG-002

**Título:*O usuario pode selecionar um valor aleatorio na prioridade *

**Severidade:*BAIXA*
**Justificativa da severidade:*alores como 0 ou negativos (ex.: -3) são semanticamente inválidos para uma escala de prioridade 1–5, mas não derrubam a aplicação. O impacto é na integridade do dado e na possível quebra de ordenações ou exibições futuras baseadas nesse campo.*

**Prioridade:*P4*
**Justificativa da prioridade:*O problema afeta apenas a validação de um campo específico e não bloqueia nenhum fluxo principal. Pode ser resolvido em sprint futura sem urgência imediata de negócio.*

**Ambiente:**
Navegador: Chrome 121.0
Sistema Operacional: Windows 11
Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
No campo "Prioridade (1-5)", digitar manualmente um valor inválido como 0, -1 ou -99
Preencher os demais campos (Título, Categoria, Prazo) normalmente
Clicar em "Adicionar tarefa"

**Resultado esperado:*Valor entre 1-5*

**Resultado obtido:*Valores aleatorios 
*

**Evidência:<img width="817" height="745" alt="image" src="https://github.com/user-attachments/assets/2f80335f-4fc1-4fa4-897a-9022394bb7c9" />

*

**Sugestão de causa raiz (opcional):**

---

## BUG-003

**Título:*tarefa com descrição duplicadas *

**Severidade:*BAIXA*
**Justificativa da severidade:*Tarefas com conteúdo idêntico geram redundância na lista, mas o usuário ainda consegue usar a aplicação normalmente. O impacto é principalmente na organização e clareza das informações exibidas, não em funcionalidades críticas.*

**Prioridade:*P4*
**Justificativa da prioridade:* duplicação de descrições não bloqueia nenhum fluxo essencial e afeta apenas a qualidade visual da lista. Pode ser tratado em sprint futura com baixa urgência.

**Ambiente:**
Navegador: Chrome 121.0
Sistema Operacional: Windows 11
Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
Preencher todos os campos com os mesmos valores (mesmo título, mesma categoria, mesmo prazo, mesma prioridade)
Clicar em "Adicionar tarefa"
Sem alterar nenhum campo, clicar em "Adicionar tarefa" novamente
**Resultado esperado:*A aplicação deve identificar a duplicata e exibir um alerta*

**Resultado obtido:*Tarefas duplicadas *

**Evidência:*<img width="779" height="751" alt="image" src="https://github.com/user-attachments/assets/7a4c4200-aebd-4836-8540-6df8a93c29ec" />
*

**Sugestão de causa raiz (opcional):**

---

<!-- Para reports adicionais, copie o bloco acima trocando o número. -->

---

## ✅ Critérios de qualidade do bug report
*(Use para conferir antes de entregar)*

- [ ✅] Título descritivo — outra pessoa entende o problema só pelo título?
- [ ✅ Passos são **numerados** e **reproduzíveis** por terceiros?
- [ ✅] Há **pelo menos uma evidência** (screenshot, GIF ou log)?
- [ ✅] Severidade tem **justificativa explícita**?
- [ ✅] Prioridade tem **justificativa explícita**?
- [ ✅] Ambiente inclui **navegador + SO**?
- [ ]✅ "Esperado vs. Obtido" deixa o gap claro?

## ✅ Checklist de qualidade dos reports

Antes de submeter, confirme em cada report:

- [ ✅] Título é específico e acionável (não `"Não funciona"`).
- [ ✅] Passos estão **numerados** e são reproduzíveis por terceiros.
- [ ✅] Há **pelo menos uma evidência** por report (imagem, GIF ou log).
- [ ✅] Severidade tem **justificativa explícita**.
- [ ✅] Prioridade tem **justificativa explícita**.
- [ ✅] Ambiente inclui **navegador + SO**.
- [ ✅] "Esperado × Obtido" deixa a diferença clara.
- [ ✅] Os 3 defeitos reportados cobrem **categorias diferentes**
      (funcional, UX, validação, persistência, etc.)
