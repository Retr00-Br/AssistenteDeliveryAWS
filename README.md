**Assistente Delivery - AWS**
- Esse projeto tem a finalidade da criação de uma assistente de IA focada em delivery, sendo totalmente realizada pela Cloud AWS.

---

## Tecnologias e Serviços AWS Utilizados

- **AWS Step Functions**: Orquestrador do fluxo de trabalho (State Machine).
- **Amazon Bedrock**: Integração do modelo LLM (*Claude 3 Haiku*) para recomendações personalizadas em tempo de execução.
- **AWS Lambda**: Validação de negócio e execução de tarefas específicas.
- **Amazon SNS**: Notificação e disparo de eventos para a cozinha/restaurante.
- **Amazon DynamoDB**: Persistência e atualização do status de rastreio em tempo real.

---

## Fluxo da State Machine (Estados)

1. **`ValidarPedido` (`Choice`)**: Checa parâmetros básicos de integridade do payload de entrada.
2. **`PersonalizarRecomendacaoBedrock` (`Task`)**: Invoca o Amazon Bedrock para gerar mensagens amigáveis e upsell baseados no histórico do cliente.
3. **`ProcessarPagamento` (`Task`)**: Chama uma função Lambda para processar a cobrança.
4. **`VerificarPagamento` (`Choice`)**: Redireciona para tratamento de erro ou para a cozinha.
5. **`NotificarCozinha` (`Task`)**: Publica o pedido pronto para produção em um tópico SNS.
6. **`AguardarPreparo` (`Wait`)**: Aguarda a sinalização/tempo de preparo.
7. **`AtualizarStatusEntrega` (`Task`)**: Grava a atualização do pedido na tabela DynamoDB.

---

## Diagrama do Fluxo (Step Functions)
![Fluxo do Step Functions](./Setep%20Function.png)

---

## Como Executar

1. Copie o código JSON do arquivo `CódigoAssistenteDelivery.json` presente neste repositório.
2. No console da AWS, vá até o **AWS Step Functions** e crie uma nova State Machine.
3. Cole o código JSON no editor de definição.
4. Inicie a execução enviando um payload de teste com os dados do pedido.

---
