# Resultados dos Testes — CardFeedback AI

## 1. Objetivo

Avaliar o funcionamento do CardFeedback AI, um assistente de inteligência artificial desenvolvido para analisar feedbacks de clientes sobre cartões de crédito, identificando sentimento, tema, prioridade, resumo e ação sugerida.

## 2. Ajustes realizados

Nos primeiros testes, o modelo utilizado não seguia consistentemente as instruções: produzia conselhos genéricos, acrescentava informações desnecessárias e nem sempre respeitava o formato solicitado.

Para melhorar o comportamento do assistente, foram realizadas duas alterações:

- **Troca do modelo:** substituímos o modelo inicial pelo Qwen2.5 1.5B, executado localmente por meio do Ollama.
- **Configuração do prompt:** no nó Basic LLM Chain, alteramos a opção *Source for Prompt (User Message)* para **Define below** e inserimos instruções explícitas de classificação.

O prompt configurado determina que o assistente:
- Classifique o sentimento como Positivo, Negativo ou Neutro.
- Escolha um tema entre as categorias definidas.
- Determine a prioridade como Alta, Média ou Baixa.
- Produza um resumo curto e uma ação sugerida para a equipe responsável.
- Não dê conselhos diretamente ao cliente.
- Não invente nomes ou informações ausentes.
- Responda somente com as cinco linhas solicitadas.

Após essas alterações, o assistente passou a respeitar melhor o formato definido e apresentou resultados satisfatórios nos testes iniciais.

## 3. Testes realizados

### Teste 1 — Cartão bloqueado

**Mensagem:** Meu cartão foi bloqueado quando tentei pagar no mercado. Não recebi aviso e o aplicativo não explica o motivo.

**Classificação esperada:**
- Sentimento: Negativo
- Tema: Bloqueio de cartão
- Prioridade: Alta

**Resultado:** O assistente identificou corretamente o sentimento, o tema principal e a prioridade nos testes após os ajustes.

### Teste 2 — Cobrança duplicada

**Mensagem:** Fui cobrado duas vezes pela mesma compra no meu cartão de crédito e ainda não recebi o estorno.

**Classificação esperada:**
- Sentimento: Negativo
- Tema: Cobrança indevida
- Prioridade: Alta

**Resultado:** O assistente identificou o problema principal e gerou uma ação sugerida para a equipe responsável.

### Teste 3 — Aplicativo indisponível

**Mensagem:** O aplicativo está fora do ar desde cedo e preciso consultar a fatura que vence hoje.

**Classificação esperada:**
- Sentimento: Negativo
- Tema: Aplicativo
- Prioridade: Alta

**Resultado:** O teste foi realizado para verificar o reconhecimento de problemas relacionados ao aplicativo e a geração de uma resposta estruturada.

### Teste 4 — Cartão perdido e compras não reconhecidas

**Mensagem:** perdi meu cartão de crédito e tive compras nesse periodo que não reconheço

**Resultado obtido:**

- Sentimento: Negativo
- Tema: Bloqueio de cartão, Cobrança indevida, Limite
- Prioridade: Alta
- Resumo: Problema com bloqueio de cartão de crédito e compras inefetivadas.
- Ação sugerida: Verifique e solucionar o problema de forma rápida.

**Avaliação:** O sentimento e a prioridade foram identificados corretamente. A categoria Cobrança indevida é pertinente ao relato, mas as categorias Bloqueio de cartão e Limite não são diretamente sustentadas pela mensagem. O resumo também alterou o sentido do relato ao mencionar compras inefetivadas, em vez de compras não reconhecidas. A ação sugerida foi genérica e poderia ser mais específica.

**Resposta esperada como referência:**

- Sentimento: Negativo
- Tema: Cobrança indevida
- Prioridade: Alta
- Resumo: Cliente perdeu o cartão e relata compras que não reconhece.
- Ação sugerida: Encaminhar as compras para análise e verificar medidas de segurança do cartão.

## 4. Análise dos resultados

A troca de modelo e a configuração do campo *Define below*, com um prompt específico, melhoraram a estrutura das respostas e a aderência às instruções.

Entretanto, o quarto teste demonstrou que o modelo ainda pode selecionar categorias adicionais sem evidência suficiente, interpretar incorretamente partes da mensagem e produzir ações sugeridas genéricas.

Esses resultados mostram que o protótipo consegue realizar a análise proposta, mas sua precisão não é garantida em todos os casos. Os testes devem considerar tanto os acertos quanto as limitações observadas.

## 5. Conclusão e melhorias futuras

O CardFeedback AI demonstra a aplicação prática de inteligência artificial local integrada ao n8n para organizar e analisar feedbacks de clientes sobre cartões de crédito.

Os ajustes realizados melhoraram o comportamento do assistente, especialmente no formato e na objetividade das respostas. O teste adicional identificou oportunidades de melhoria na seleção de temas, na fidelidade dos resumos e na especificidade das ações sugeridas.

Como próximos passos, recomenda-se aprimorar as instruções de classificação e ampliar a quantidade de testes com mensagens variadas, comparando as respostas produzidas com classificações de referência.

O projeto constitui um protótipo funcional para fins de demonstração e pode evoluir com novas validações e melhorias de precisão.

