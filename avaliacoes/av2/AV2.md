# Entrega individual — AV2

Estudante: Heitor José Andrade de Oliveira · Data: 01/10/2026 · Via: inspeção / execução opcional
**Limites:** análise até duas páginas; anexo técnico até duas páginas. [Enunciado](README.md).

## Análise

**1. Recorte e requisito.** Função/tarefa, quem usa o resultado e limites de entrada: A função avaliada é pode_visualizar_proposta(chamado, departamento). Quem usa o resultado é a pessoa que consulta chamados e o sistema que decide o que exibir. As entradas são válidas: departamentos Oficina e Laboratório, estados aberto, em_andamento e fechado, e impacto e urgência de 1 a 3. Autenticação, persistência e validação externa ficam fora do escopo.
R3/R4 em minhas palavras e critério de aceite definido antes da verificação: R3 em minhas palavras: O acesso depende apenas de o departamento da pessoa ser igual ao do chamado. Estado e prioridade não entram na decisão. R4 exige que a documentação descreva esse mesmo comportamento. Critério de aceite, definido antes de olhar o candidato: o código e o texto são aceitos se, para toda combinação de departamento (igual/diferente) e estado (aberto/fechado), o retorno for True somente quando o departamento for igual. A documentação não pode afirmar nenhuma restrição por estado.

**2. Estratégia.** Eixos da matriz, motivo dos quatro casos e o que mantenho constante: Os eixos são departamento (igual/diferente) e estado (aberto/fechado), com as quatro combinações. Mantive constantes o solicitante (Oficina) e os valores de impacto e urgência de cada registro (V-01 e V-02 com 1/1, V-03 e V-04 com 3/3). Esses valores só servem para mostrar que não afetam o resultado.
Caso decisivo e caso de controle, com justificativa: O caso decisivo é T2 (mesmo departamento, fechado). É a única combinação em que o candidato pode divergir de R3 por causa do estado, pois a cláusula != "fechado" só age nessa célula. O caso de controle é T3 (departamento diferente, aberto). O contrato e o candidato devem concordar nele, porque o teste de departamento é o mesmo e o estado é o permitido pelo candidato.

**3. Evidência e interpretação.** Principais achados com referência a linhas T1–T4 e trechos E1–E3 do anexo: T1, T3, T4 coincidem com R3. T1 retorna True e T3 e T4 retornam False, como esperado. T2 diverge de R3. O contrato espera True, mas o candidato retorna False (E2). O erro está na condição adicional estado != "fechado", que R3 proíbe de forma expressa ("independentemente de estado"). A documentação (E3) é coerente com o código, mas não com R3. Ela diz que chamados fechados ficam indisponíveis, o que contradiz R3 e viola R4. As demais afirmações estão corretas: outros departamentos não são exibidos, e impacto e urgência não alteram a decisão.
Relação entre contrato, comportamento do código e documentação: Contrato × código: o código implementa R3 mais uma regra extra. Quando o departamento é diferente, o resultado é False por qualquer um dos dois critérios e a regra extra é invisível (T3, T4). Quando é igual e o chamado está aberto, ela também não age (T1). Ela só aparece na célula "igual / fechado" (T2), e é ali que o código viola R3: esconde do próprio departamento um chamado que o contrato manda mostrar.
Contrato × documentação (E3): o texto afirma que "chamados fechados ficam indisponíveis" e fala em "chamados ativos de seu próprio departamento". Ambas as formulações contradizem R3 e, por consequência, R4, que exige que a documentação descreva o mesmo comportamento do contrato. As outras duas afirmações do texto (chamados de outros departamentos não são exibidos; impacto e urgência não alteram a decisão) são compatíveis com R3.
Código × documentação: os dois são coerentes entre si. O texto descreve fielmente o que o código faz, inclusive o comportamento errado. Isso tem uma consequência para a decisão: a concordância entre código e documentação não é evidência de correção. Quem lesse só a documentação, ou só conferisse o código contra ela, aprovaria a proposta. O defeito só aparece quando ambos são confrontados com o contrato.

**4. Decisão comparada.** Encaminhamento do código e da documentação, com fundamento: Rejeitar o código e rejeitar a documentação. Ambos descrevem e implementam uma regra diferente de R3.
Alternativa considerada / comparação sob o mesmo critério: Corrigir código e texto. Remover and chamado["estado"] != "fechado" e remover da documentação a menção a "ativos" e à indisponibilidade de fechados. Resultado: T1–T4 conformes
Ajuste proposto, se aplicável, e revalidação (linhas do anexo): Revalidação da alternativa acima: T1 True, T2 True, T3 False, T4 False, todos conformes a R3, com status inferido por inspeção.
Responsável pelo aceite e condição para rever a decisão: Responsável pela manutenção de Fila Clara (dono do requisito R3). Condição para rever a decisão: (a) alteração formal de R3 para ocultar chamados fechados, caso em que a alternativa B seria reavaliada; ou (b) execução do código que contradiga minha inferência.___

**5. Procedência e limites.** Artefatos didáticos simulados utilizados: Contrato, candidato, documentação e registros V-01 a V-04, todos didáticos e fictícios, fornecidos no enunciado.
O que observei em execução / inferi por inspeção / apenas propus: Nada. Todos os retornos foram inferidos por inspeção. A alternativa foi apenas proposta, e sua revalidação também é inferida.
Limite concreto da cobertura e consequência para minha decisão: São quatro casos e nenhum com em_andamento. Por inspeção o código só compara com "fechado", então em_andamento deve se comportar como aberto, mas isso não foi testado. Também não foram testados Laboratório com variações de grafia nem diferentes valores de impacto e urgência (a independência de prioridade vem de o código não ler esses campos). Consequência: a rejeição por T2 é sólida, porque a divergência é lógica e direta. Já o aceite da alternativa A só vale para o que foi coberto. Isso não permite concluir nada sobre segurança de um sistema real.
IA: ferramenta-modelo visível: Claude (Claude Sonnet 5.5); data: 01/10/2026; tarefa/contexto: não informado; trecho aproveitado: não informado; verificação/intervenção próprias: Ortografia e diminuicao em linguagem exageradamente tecnica. Metadado indisponível: “não informado”.

## Anexo técnico — trechos essenciais

**Dados e condições comuns:** referência aos registros de insumos.md ou dicionários completos, departamento solicitante e valores mantidos: Registros V-01 a V-04 do enunciado; solicitante = "Oficina" em todos os casos; impacto e urgência conforme os registros.

| Caso | Entrada/referência + solicitante | Relação de departamento / estado | Esperado por R3 | Retorno do candidato | Status observado/inferido | Interpretação |
|---|---|---|---|---|---|---|
| T1 |V-01 (Oficina, aberto), "Oficina" | Igual / aberto |True |True |Inferido |Conforme |
| T2 |V-02 (Oficina, fechado), "Oficina" | Igual / fechado |True |False |Inferido |	Divergência: o candidato esconde chamado do próprio departamento |
| T3 |V-03 (Laboratório, aberto), "Oficina" | Diferente / aberto |False |False |Inferido |Conforme |
| T4 |V-04 (Laboratório, fechado), "Oficina" | Diferente / fechado |False |False |Inferido |Conforme |

**E1 — trecho do contrato e localização:** "pode_visualizar permite acesso somente à pessoa do mesmo departamento do chamado, independentemente de estado ou prioridade."
**E2 — trecho do código + percurso lógico de um caso decisivo e um controle:**  
```python
return (chamado["departamento"] == departamento
        and chamado["estado"] != "fechado")
```
T2 (decisivo): "Oficina" == "Oficina" dá True; "fechado" != "fechado" dá False; True and False dá False. R3 esperava True.
T3 (controle): ```"Laboratório" == "Oficina"``` = False, e o and curto-circuita, retornando False. O estado nem é avaliado.
**E3 — trecho da documentação e confronto com R3/código:** "chamados fechados ficam indisponíveis". Isso contradiz R3 ("independentemente de estado") e, portanto, R4. As frases sobre outros departamentos e sobre impacto e urgência são consistentes com R3.
**Execução, se escolhida — ambiente, comando e trecho de saída:** não realizada.
**Alternativa/ajuste e revalidação:** Comportamento proposto: return chamado```["departamento"] == departamento```. Texto proposto: "A função permite que uma pessoa visualize chamados do seu próprio departamento, em qualquer estado. Chamados de outros departamentos não são exibidos. Impacto e urgência não alteram essa decisão."; 
T1–T4 após ajuste (esperado/retorno/status):
| Caso | Esperado | Retorno | Status |
|------|----------|---------|--------|
| T1   | True     | True    | Inferido |
| T2   | True     | True    | Inferido |
| T3   | False    | False   | Inferido |
| T4   | False    | False   | Inferido |; 

limite: A revalidação é por inspeção. Os mesmos casos não cobrem em_andamento nem variações de grafia.

**Checklist:** [X] 4 combinações; [X] critérios prévios; [X] código e texto; [X] status; [X] alternativa; [X] limites/IA; [X] 2+2 páginas.
