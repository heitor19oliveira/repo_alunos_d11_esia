# Registro individual — AV1.3

**Limite: uma página.** Estudante: Heitor José Andrade de Oliveira — Data: 01/10/2026
**O que a listagem e a documentação precisam cumprir, conforme R2/R4:** Incluir aberto e em_andamento, excluir fechado e preservar a ordem de entrada. O texto da documentação deve descrever exatamente esse comportamento.

| Caso / estado a verificar | Entrada (IDs e ordem) | IDs esperados na ordem | Obrigação de R2 e como verificar |
|---|---|---|---|
| 1 / aberto |[TR-33] |[TR-33] |Incluir aberto. Conferir que TR-33 aparece na saída. |
| 2 / em_andamento |[TR-31] |[TR-31] |Incluir em_andamento. Conferir que TR-31 aparece na saída. |
| 3 / fechado |[TR-32] |[TR-32] |Excluir fechado. Conferir que a saída é lista vazia. |

**Entrada combinada TR-31, TR-32, TR-33 → IDs esperados:** [TR-31, TR-33]
**Como conferiria a ordem (compare a posição dos IDs na entrada e na saída esperada):** Na entrada, TR-31 está na posição 1 e TR-33 na posição 3. Na saída esperada, TR-31 vem antes de TR-33, a mesma ordem relativa. TR-32 sai sem alterar a posição relativa dos outros dois. Se a saída fosse [TR-33, TR-31], a ordem teria sido violada, por exemplo por ordenação por impacto ou urgência.
**Documentação proposta (até três frases):** "A listagem inclui os itens com estado aberto e em_andamento e exclui os itens com estado fechado. Os itens que permanecem mantêm a mesma ordem em que entraram. Nenhuma reordenação por impacto ou urgência é aplicada."

**Etapa em que admitiria IA / tarefa que ela faria / pessoa responsável por conferir:** Rascunho dos três casos de teste e da documentação a partir de R2 e R4. A tarefa delegada é gerar a primeira versão. Eu sou a pessoa responsável por conferir.
**O que essa pessoa deve verificar antes de aprovar:** Aplicar R2 manualmente a cada registro (estado → incluído ou excluído), recalcular a saída combinada, comparar a posição de cada ID entre entrada e saída, e ler a documentação para confirmar que descreve só as três obrigações de R2, sem acrescentar nem omitir nenhuma.
**Alternativa sem IA e comparação:** Escrever tudo manualmente. Leva mais tempo e depende só da minha leitura, sem segunda versão para comparar. Com IA, o rascunho é mais rápido, mas há risco de a IA inventar regra (como ordenar por prioridade), então a conferência manual é indispensável.
**O que os casos não verificam e o que me faria rever a aprovação:** Não cobrem entrada vazia, vários registros do mesmo estado, empates, IDs duplicados, estados fora do contrato nem execução real do código. Eu reveria o aceite se R2 mudasse, se surgisse um novo estado ou se uma execução real divergir da saída esperada.

**Origem dos dados e como fiz a análise:** entrada fictícia do enunciado; esperado por contrato: Saídas calculadas por R2; inspeção própria: conferi estado e posição de cada registro; execução opcional (comando/resultado, se houver): não realizada(saídas esperadas calculadas por R2, sem resultado observado).
**Uso de IA neste registro:** ferramenta-modelo visível: Claude (Claude Sonnet 5.5); contexto/tarefa: Preenchimento do modelo a partir do enunciado; trecho aproveitado e minha verificação: Casos, saída combinada e documentação, conferidos manualmente contra R2.

**Revisão:** [X] três estados; [X] ordem; [X] texto; [X] aceite/limite; [X] uma página.
