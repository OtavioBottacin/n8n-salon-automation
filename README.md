# WhatsApp Bot State Machine (n8n + PostgreSQL)

Um sistema profissional de automação de atendimento via WhatsApp, projetado para rotear conversas de forma inteligente entre um bot de autoatendimento e o atendimento humano, sem conflitos.

## O Problema
Em cenários de atendimento ao cliente via WhatsApp, bots comuns costumam interromper o atendente humano, criando uma experiência frustrante para o usuário final. 

## A Solução
Implementação de uma lógica de **Máquina de Estados** (State Machine) utilizando um banco de dados relacional. O bot verifica o status da conversa em milissegundos antes de agir, garantindo que ele só responda quando o cliente estiver fora de um atendimento humano ativo.

## Arquitetura e Tecnologias
* **n8n:** Orquestração do fluxo e lógica condicional.
* **PostgreSQL:** Persistência de dados e controle de estado (`novo`, `escolhendo`, `aguardando`, `encerrado`).
* **Evolution API:** Comunicação com o WhatsApp via Webhooks.
* **Docker / Easypanel:** Hospedagem independente dos contêineres.

## Destaques Técnicos
* **Tratamento de Exceções:** Uso de Regex (`^[1-7]$`) para validar entradas do usuário e tratar opções inválidas em loop.
* **Filtro de Eventos:** Bloqueio nativo de eventos irrelevantes (como status de "digitando") para evitar processamento desnecessário no servidor.
* **UPSERT Queries:** Operações blindadas no banco de dados (`ON CONFLICT DO UPDATE`) para prevenir erros em clientes não cadastrados.

## Como importar
Basta fazer o download do arquivo `fluxo-bot.json` deste repositório e utilizar a função "Import" diretamente na sua instância do n8n.
