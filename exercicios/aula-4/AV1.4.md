# Registro individual — AV1.4

**Limite: uma página.** Estudante: Heitor José Andrade de Oliveira — Data: 11/10/2026
**Critério de aceite por R2:** A listagem inclui aberto e em_andamento, exclui fechado e preserva a ordem de entrada (sem reordenar por prioridade)

| Entrada | IDs esperados por R2 | IDs do candidato | Status: inferido/observado | Mecanismo/trecho essencial |
|---|---|---|---|---|
| TR-41, TR-42, TR-43, TR-44 |TR-41, TR-42, TR-44 |TR-42,TR-44,TR-41 |Inferido(leitura) | ```sorted(ativos, key=lambda c: c["impacto"] + c["urgencia"], reverse=True)``` A ordenção proposta pelo candidato não preserva a ordem de entrada pois coloca TR-41 por último, violando R2.|

**Teste entregue — o que verifica e o que não consegue distinguir:** Ele verifica que TR-43 (fechado) é excluído e que os três ativos aparecem. Não distingue uma função que cumpre R2 de uma que a descumpre quanto à ordem. A entrada do teste (TR-42, TR-44, TR-41, TR-43) já está em ordem decrescente de escore (6, 4, 2). Assim, “preservar a ordem de entrada” e “ordenar por escore” produzem o mesmo resultado, e o teste passa nos dois casos.
**Trecho do teste (entrada e comparação de IDs) que sustenta minha análise:** Entrada na ordem TR-42, TR-44, TR-41, TR-43; asserção: IDs retornados == ```["TR-42", "TR-44", "TR-41"]```.
**Decisão (aceitar, aceitar com condições ou rejeitar) e motivo:** Rejeitar. Candidato ordena os chamados por escore e não garante a ordem de entrada exigida por R2. O teste entregue não detecta essa falha porque, naquela entrada, a ordem por escore coincide com a ordem esperada.
**Comparação entre manter e ajustar / responsável pelo aceite:** Manter sorted prioriza os chamados de maior escore, mas viola a ordem de entrada exigida por R2. Ajustar removendo a ordenação atende ao contrato. A decisão de alterar R2, caso a prioridade deva determinar a ordem, cabe ao responsável pelo requisito; até essa aprovação, deve prevalecer R2.
**Ajuste proposto (texto ou código):**
```python
def listar_ativos_proposta(chamados):
    return [c for c in chamados if c["estado"] in ("aberto", "em_andamento")]
```

| Caso para conferir o ajuste: entrada e ordem | IDs esperados | Resultado previsto ou observado / status |
|---|---|---|
|TR-41, TR-42, TR-43, TR-44 (ordem original) |TR-41, TR-42, TR-44 |TR-41, TR-42, TR-44: previsto por leitura |

**Limite remanescente e condição para rever o parecer:** A análise foi feita só por leitura, sem executar o código, e não cobre entradas inválidas ou outros valores de estado. Reviso a decisão se a execução do ajuste em cópia isolada divergir do previsto, ou se R2 for alterado oficialmente para incluir ordenação por prioridade.
**Origem dos dados e da análise:** candidato/teste/entrada simulados; método próprio: inspeção / execução; comando e trecho de saída, se executado: não realizado.
**Uso de IA neste registro:** ferramenta-modelo:  Claude (Claude Sonnet 5.5) + Github Copilot; tarefa/contexto: Claude me ajudou no entendimento do enunciado da atividade e o Github Copilot me auxilou na analise por inspeção dos trechos de código; trecho aproveitado e minha verificação: O ajuste proposto em codigo Python foi fornecido pela IA do Github Copilot e eu realizei a verificacao de sintaxe e lógica propostas.

**Revisão:** [X] comparação com R2; [X] alcance do teste; [X] ajuste/revalidação; [X] status; [X] uma página.
