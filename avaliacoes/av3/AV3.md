# AV3 — Parecer integrador fundamentado

Estudante: Heitor José Andrade de Oliveira · Data: 12/10/2026 · Caso/recorte: Fila Clara — Assistência de IA para testes e documentação de regras internas

**Limites:** parecer até três páginas; evidências/referências até duas páginas.

## Parecer

### 1. Recomendação e problema

Recomendo uso condicionado de IA assistiva para a tarefa de propor testes, revisar documentação e sugerir explicações de regra em Fila Clara, cujo beneficiário é a equipe de manutenção e o resultado esperado é uma base de evidência mais rápida, sem perder a correção do contrato. As restrições relevantes são: dados sintéticos, ausência de implantação em produção, ausência de autenticação real, e obrigação de verificar qualquer sugestão contra as regras R1–R4 do contrato e contra os registros de AV1/AV2 antes de qualquer aceitação.

| Alternativa | Processo e recursos | Benefício esperado / pressuposto | Limite, consequência do erro e esforço de verificação |
|---|---|---|---|
| A — sem IA | A equipe lê o contrato, escreve testes manualmente e revisa a documentação em dupla. | Controle total e baixo risco de contextualização errada. | Maior esforço manual, maior demora e maior chance deixar inconsistência artesanal sem checagem automatizada. |
| B — IA assistiva, com validação humana | A IA sugere matrizes de casos, redações de documentação e listas de verificação; a pessoa responsável compara com R1–R4 e com registros existentes. | Acelera a triagem inicial e amplia cobertura de casos sem substituir a decisão humana. | Se usada sem critério, pode reforçar interpretação errada de regra, inventar casos sem base ou ocultar uma exceção. O esforço de verificação continua exigido. |

Minha comparação e razão para a recomendação: a tarefa não é “inventar regras”, mas “formalizar um contrato já conhecido e validar se a implementação e a documentação o respeitam”. Nesse cenário, a IA é útil como aceleradora de primeira leitura, mas não pode decidir se uma regra está correta. O custo de erro é alto porque a regra de visibilidade afeta acesso a chamados internos; um erro de interpretação pode criar acesso indevido ou ocultar falhas. Portanto, a recomendação é condicionada: uso com escopo limitado, revisão humana, e exigência de evidência objetiva antes da adoção.

### 2. Autonomia e responsabilidade

Etapa/tarefa assistida, se recomendada: a IA pode sugerir uma matriz de testes, uma redação inicial de documentação e uma checklist de contradições entre código e contrato; pode também resumir o que o AV2 observou, mas sempre como proposta, não como conclusão final.

O que permanece sob aceite humano / critério e responsável: a pessoa designada para manutenção do caso (gestor de Fila Clara ou responsável técnico) decide se a sugestão entra no arquivo, na revisão do código ou na documentação oficial. O criterioso é a conformidade com R1–R4, com os registros do caso e com a regra de afirmação responsável: qualquer trecho que contradiga o contrato ou o que foi validado na evidência deve ser recusado, não apenas melhorado.

Condição de intervenção, tratamento de exceção e reversibilidade/recusa: se a IA produzir uma saída ambígua, inventar um caso fora do conjunto válido, ou sugerir uma regra que conflite com a base de dados sintética, a intervenção deve ser imediata. A saída inadequada deve ser rejeitada, revertida para a versão anterior ou reescrita manualmente. Em termos práticos, a regra é simples: “sem evidência rastreável, sem aceite”. Isso preserva reversibilidade e evita que a IA passe a ser responsável pela decisão final.

### 3. Verificação e contraponto

Evidência E1 do anexo: o registro de AV2 e a matriz de visibilidade de `pode_visualizar`, confrontando `R3` com a implementação; o critério é que a visibilidade deve ser restrita ao mesmo departamento, independentemente de estado ou prioridade. O resultado observado foi que a regra de negócio foi interpretada como “mesmo departamento ou impacto + urgência >= 5”, o que contradiz o texto do contrato e o objetivo didático do caso. A interpretação que sustenta a recomendação é direta: quando a regra do negócio é simples e a biblioteca de testes e documentação exige precisão, a IA precisa receber um contrato explícito e um critério de validação; sem essa etapa, ela reforça a mesma falha que o projeto já mostrou.

Limitação ou evidência contrária E2: o caso é fictício e os dados são sintéticos. Isso limita a generalização para sistemas reais, porque não há usuários reais, dados de produção, nem validação operacional com diferentes perfis de acesso. O efeito na recomendação é restringi-la a um uso assistivo e controlado, não a uma adoção “pronta para produção”. A condição que mudaria a recomendação seria um contexto com dados reais, política formal de acesso, responsável definido e evidência de uso em ambiente controlado, o que ainda não acontece em M1–M6.

### 4. Riscos e mecanismos

| Risco e consequência no recorte | Mecanismo | Responsável | Evidência e como conferir o controle | Exceção/interrupção |
|---|---|---|---|---|
| 1. Acesso indevido por interpretação errada da regra de visibilidade. Consequência: um chamado pode ser exibido a pessoa de outro departamento apenas porque a soma de impacto e urgência é alta. | Verificação automática de casos de fronteira e checklist de regra por `R3`/`R4`; revisão de cada sugestão de IA contra a matriz de AV2. | Gestor de manutenção e responsável técnico de Fila Clara. | Executar a matriz (mesmo departamento/aberto; mesmo departamento/fechado; departamento diferente/aberto; departamento diferente/fechado) e registrar esperado versus retorno. Qualquer discrepância exige rejeição. | Se o critério não for atendido em um caso decisivo, a proposta de IA é interrompida e enviada para revisão manual antes de qualquer aprovação. |
| 2. Documentação e testes gerados por IA que parecem corretos, mas não são conformes ao contrato. Consequência: equipe gera confiança falsa e leva a decisões de implementação baseadas em texto plausível e não verificado. | Geração de sugestões como rascunho; revisão por human reviewer; exigência de rastreio para cada item gerado: regra, evidência, resultado esperado, status da checagem. | Líder de qualidade/maintainer e revisor designado. | Comparar cada sugestão com os três registros do caso e com o contrato. O controle é comprovado quando cada item gerado tem origem e critério explícitos. | Se houver item sem rastreio ou com contradita ao contrato, o fluxo é interrompido até correção e revalidação. |

### 5. Maturidade e próximo passo

Objeto e estágio: a iniciativa está em estágio inicial, com artefato demonstrável, responsável designado, revisão definida, duas semanas planejadas e zero execução com usuários. Isso indica maturidade baixa a moderada para uso assistivo, mas não para decisão autônoma em ambiente real. A definição adotada é “assistência limitada a geração e revisão de testes e documentação, sempre sob validação humana e sem processamento de dados externos”.

Fatos que sustentam: (i) a gestão do caso menciona lacunas de governança e ausência de confirmação sobre dados externos; (ii) M1–M6 reportam zero execução com usuários; (iii) a verificação de AV2 demonstrou que a regra de visibilidade pode ser interpretada errada por implementação ou por documentação inadequada; (iv) o contrato R3/R4 exige comparação constante com critérios explícitos.

Estágio rival e motivo da distinção: um estágio “mais avançado” seria uso operacional com política de acesso definida, dados controlados e execução supervisionada. A distinção é clara: aqui não há evidência suficiente para uso além de apoio assistivo, porque a equipe ainda não validou o contexto de governança e uso.

Lacuna: ainda não foi demonstrada a capacidade do fluxo de IA de manter consistência com contratos em condições reais de operação, especialmente quando regras de acesso e dados externos entram em cena.

Passo proposto — tarefa, participantes, duração, dados e responsável: em uma semana, a equipe cria uma matriz de cinco a dez casos de regras (R1–R4), pede à IA para sugerir rascunho de testes, e cada item é revisado por responsável técnico em uma review de 30 minutos. Dados: contrato, registros de AV1/AV2 e chamados sintéticos. Responsável: gestor designado do caso + revisor de qualidade.

Métrica (fórmula/unidade e, se taxa, numerador/denominador): taxa de conformidade do rascunho = número de itens gerados pela IA aceitos após verificação / total de itens sugeridos. Se a equipe sugerir 20 itens e 18 forem aprovados sem correções, a taxa é 90% (18/20). A comparação referencia um baseline manual do mesmo conjunto de regras: a adoção só avança se a taxa de conformidade não cair abaixo de 90% e não houver nenhum item com conflito direto com R3/R4.

Coleta e referência de comparação: medir em duas semanas, com as mesmas regras e dados sintéticos, e comparar com a execução manual anterior. Limite da medida: a métrica mede consistência documental e de teste em ambiente controlado, não produtividade real, segurança de produção ou aceitação de usuários.

Condição proposta de avanço / quem decide: avanço apenas quando a taxa de conformidade atingir 90% e os casos decisivos de acesso forem aprovados sem exceção; a decisão cabe ao responsável técnico e ao gestor do caso.

Condição proposta de interrupção / quem age: se houver qualquer divergência direta com o contrato em caso decisivo, ou se houver ausência de rastreio de evidência, o uso da IA é interrompido e a tarefa retorna ao processo manual; o responsável técnico atua imediatamente.

### 6. Fundamentação aplicada

- F1: Fan et al., “Large Language Models for Software Engineering: Survey and Open Problems”, v4, 2023, Introdução e Conclusão. A literatura reconhece que LLMs ajudam muito em geração e revisão de código, mas a confiabilidade e a correção continuam sendo problemas-chave. Decisão do parecer a que se aplica: a IA pode acelerar produção de testes e documentação, mas não deve decidir o resultado sem validação. O que a fonte sustenta: capacidade útil, mas risco de erro e falta de garantia de correção. Minha inferência: em Fila Clara, a natureza simples mas normativa do contrato exige verificação humana explícita, porque o ambiente de apoio não substitui regras de negócio. Limite/contraponto: a literatura não prova que a mesma confiabilidade se mantém em um contexto de dados reais, com regras de segurança e governança ainda não confirmadas.
- F2: Hou et al., “Large Language Models for Software Engineering: A Systematic Literature Review”, v6, 2024, Introdução e Conclusão. A revisão mostra que a avaliação de tarefas de engenharia de software com LLMs depende muito do contexto, do benchmark e da validação específica; a performance geral não equivale a confiabilidade operacional. Decisão do parecer a que se aplica: o uso deve ser acoplado a um critério de aceite e a uma métrica controlada. O que a fonte sustenta: a qualidade do uso varia conforme tarefa, evidência e critérios. Minha inferência: como o caso Fila Clara tem regras de acesso e documentação bem definidas, a IA pode ser útil em um escopo delimitado e controlado, desde que o responsável valide cada saída. Limite/contraponto: o estudo não elimina o risco de certos erros de interpretação quando o contexto institucional ainda não está estável.

## Anexo — evidências, referências e procedência

**E1 — origem/atividade, arquivo ou identificação e trecho exato:** AV2 — etapa de verificação da função `pode_visualizar`; `caso/regras.md` — R3; `caso/chamados.json` — registros sintéticos e `caso/fila_clara.py` — implementação. Entrada/fato: mesmo departamento ou impacto+urgência >= 5; critério: R3 exige acesso somente ao mesmo departamento, independentemente de estado ou prioridade; resultado: implementação e documentação divergentes; status observado/inferido: inferido por inspeção e por comparação com os dados/contrato. 

**E2 — origem e trecho ou limitação/contraponto da evidência:** a situação é fictícia, com dados sintéticos, sem execução com usuários e sem dados reais. Isso limita a aplicação para ambientes reais, mas não invalida o uso didático para propor controle de risco e validação humana.

**Outros trechos essenciais de apoio às decisões, se necessários:** `caso/regras.md` — R2 e R4; `caso/fila_clara.py` — a função `prioridade` e o filtro de ativos; `chamados.json` — casos sintéticos de estados `aberto`, `em_andamento` e `fechado`.

**F1 — referência de L0:** autores: Fan et al.; título: “Large Language Models for Software Engineering: Survey and Open Problems”; ano/versão: v4, 2023; seção/página consultada: Introdução e Conclusão; referência/link identificável: arXiv:2310.03533v4. 

**F2 — referência de L0:** autores: Hou et al.; título: “Large Language Models for Software Engineering: A Systematic Literature Review”; ano/versão: v6, 2024; seção/página consultada: Introdução e Conclusão; referência/link identificável: arXiv:2308.10620v6.

**Procedência:** materiais simulados reaproveitados: contrato R1–R4, registros de AV1/AV2, caso Fila Clara e dados sintéticos; observações próprias: a IA deve ser assistiva e não decisória; inferências: recomendação de uso condicionado e limites de maturidade; passos e metas propostos: matriz de regra, revisão humana, métrica 90% de conformidade. 

**IA:** assistente de escrita/estruturação usado para ordenar e revisar linguagem; data: 12/10/2026; tarefa/contexto: revisão do parecer de AV3; trecho aproveitado: estrutura e estilo do texto; verificação e intervenção próprias: cada afirmação foi confrontada com o contrato, com o caso e com as referências L0; melhoras foram reavaliadas em relação à regra e à evidência. 

**Checklist:** [x] alternativas; [x] autonomia; [x] evidência/contraponto; [x] dois riscos; [x] maturidade/métrica; [x] duas fontes aplicadas; [x] procedência; [x] 3+2 páginas.
