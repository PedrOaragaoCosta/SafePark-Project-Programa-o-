# Safepark: Inteligência de Vagas na Zona Azul

## Documentação da Entrega 1 da AV2

**Fundamentos de Programação • ADM Tech**  
**Lente 8 — Mobilidade Inteligente & Programação**  
**Centro do Recife**  
**Planejamento da v0.1 — 16/11/2026**

> Os dados de vagas, ocupação e pontos desta versão são simulados para a v0.1.

---

## 1. Visão geral do projeto

### Contexto e problema

Quem vai de carro ao Centro do Recife costuma procurar vaga sem saber previamente onde existe maior disponibilidade. Essa busca pode aumentar o tempo de circulação e contribuir para o congestionamento.

### Usuário principal

Estudantes da CESAR School e trabalhadores que vão de carro ao Centro do Recife.

### Objetivo

Permitir que o motorista informe seu destino antes de sair e consulte a ocupação das micro-regiões, identificando quais estão mais livres para decidir onde procurar uma vaga.

### Recorte

O projeto trabalha com as vagas de Zona Azul e garagens do Centro do Recife. Na v0.1 serão utilizadas quatro micro-regiões com dados simulados.

A utilização de câmeras com visão computacional fica prevista para uma etapa futura e não faz parte da v0.1.

---

## 2. História de usuário e esclarecimentos

### História de usuário

**Como motorista que vai de carro ao Centro do Recife, quero informar meu destino antes de sair de casa e visualizar a ocupação da Zona Azul e as micro-regiões mais livres, para decidir onde procurar vaga sem rodar às cegas.**

### História complementar

**Como motorista, quero avisar que liberei uma vaga e receber pontos, para ser recompensado por ajudar a manter os dados atualizados.**

### Esclarecimentos

- **Quem usa:** motoristas, principalmente estudantes da CESAR School e trabalhadores que vão de carro ao Centro.
- **Origem dos dados na v0.1:** dados simulados de quatro micro-regiões; não haverá câmeras nesta versão.
- **Destino:** uma das micro-regiões disponíveis.
- **Avisos falsos:** outro motorista pode denunciar uma vaga informada como liberada.
- **Denúncia sem câmeras:** na v0.1, uma denúncia é suficiente para aplicar a penalidade.
- **Pontos e limites:** são valores simulados e poderão ser ajustados após a validação.

---

## 3. Requisitos funcionais

| ID | Comportamento esperado | Prioridade |
|---|---|---|
| RF01 | Exibir as quatro micro-regiões, com vagas totais, vagas ocupadas e ocupação. | Essencial |
| RF02 | Permitir escolher uma micro-região como destino. | Essencial |
| RF03 | Mostrar o percentual de ocupação do destino e da Zona Azul. | Essencial |
| RF04 | Classificar as micro-regiões e mostrar primeiro as mais livres. | Essencial |
| RF05 | Permitir registrar o aviso de saída de uma vaga. | Essencial |
| RF06 | Exibir pontos e dias grátis do motorista. | Essencial |
| RF07 | Permitir denunciar uma vaga informada como liberada e aplicar a penalidade. | Essencial |
| RF08 | Manter os dados separados da interface para facilitar futuras mudanças na fonte de dados. | Desejável |

---

## 4. Requisitos não funcionais

| ID | Condição exigida | Como conferir |
|---|---|---|
| RNF01 | Textos, orientações e mensagens em português. | Percorrer o fluxo e ler os textos. |
| RNF02 | Percentuais com `%` e vagas no formato “120 de 200”. | Conferir mapa e lista. |
| RNF03 | Destino, ocupação e classificação na mesma visualização. | Escolher um destino e conferir as três informações. |
| RNF04 | Classificação escrita como Livre, Moderada ou Cheia. | Abrir o mapa e conferir os textos. |
| RNF05 | Fluxo acessível gratuitamente pelo navegador em computador e celular. | Abrir e testar em diferentes tamanhos de tela. |
| RNF06 | Informar claramente que os dados são simulados. | Localizar o aviso na aplicação. |

---

## 5. Regras de negócio e dados

### Dados simulados

| Micro-região | Vagas totais | Ocupadas | Ocupação | Classificação |
|---|---:|---:|---:|---|
| Recife Antigo (CESAR School) | 200 | 120 | 60% | Moderada |
| Santo Antônio | 120 | 60 | 50% | Livre |
| São José | 100 | 85 | 85% | Cheia |
| Boa Vista | 180 | 72 | 40% | Livre |
| Zona Azul (soma) | 600 | 337 | 56% | Livre |

> Esses valores são simulados e não representam o inventário real de vagas do Recife.

### Regras

- **RN01:** o aplicativo trabalha com quatro micro-regiões fixas.
- **RN02:** ocupação = vagas ocupadas ÷ vagas totais × 100, arredondada para inteiro.
- **RN03:** a ocupação da Zona Azul usa a soma das vagas ocupadas dividida pela soma das vagas totais.
- **RN04:** abaixo de 60% = Livre; de 60% a 84% = Moderada; a partir de 85% = Cheia.
- **RN05:** a lista mostra primeiro a menor ocupação; em empate, usa ordem alfabética.
- **RN06:** cada aviso de saída válido reduz em 1 as vagas ocupadas.
- **RN07:** cada aviso válido concede 10 pontos; a cada 100 pontos, o motorista ganha 1 dia grátis.
- **RN08:** um motorista pode denunciar o aviso de outro uma vez.
- **RN09:** denúncia aceita contesta o aviso, devolve a vaga para ocupada e desconta 30 pontos, sem saldo negativo.

---

## 6. Critérios de aceitação

- **CA01:** ao abrir o aplicativo, devem aparecer as quatro micro-regiões, vagas totais/ocupadas e o aviso de dados simulados.
- **CA02:** Recife Antigo deve apresentar 60%, classificação Moderada e Zona Azul em 56%.
- **CA03:** São José deve apresentar 85%, classificação Cheia e indicar Boa Vista como a mais livre.
- **CA04:** a ordem das regiões mais livres deve ser Boa Vista (40%), Santo Antônio (50%), Recife Antigo (60%) e São José (85%).
- **CA05:** um aviso válido de saída em Santo Antônio reduz a ocupação de 60 para 59 vagas e concede 10 pontos.
- **CA06:** com 90 pontos, um aviso válido leva o motorista a 100 pontos e libera 1 dia grátis.
- **CA07:** não deve ser possível registrar saída quando não houver vaga ocupada registrada.
- **CA08:** uma denúncia aceita deve contestar o aviso, atualizar a ocupação e aplicar a penalidade.
- **CA09:** o motorista não pode denunciar o próprio aviso.
- **CA10:** o saldo de pontos nunca pode ficar abaixo de zero.

---

## 7. Escopo e tecnologia da primeira versão

### Incluído na v0.1

- Mapa esquemático com quatro micro-regiões.
- Dados simulados.
- Escolha de destino.
- Cálculo e classificação da ocupação.
- Lista das regiões mais livres.
- Aviso de saída de vaga.
- Sistema de pontos e dias grátis.
- Denúncia de vaga ocupada.
- Penalização de avisos considerados incorretos.
- Aviso de que os dados são simulados.

### Fora da v0.1

- Câmeras e visão computacional.
- Detecção real de vagas em tempo real.
- GPS e rotas reais.
- Login e cadastro completo.
- Servidor e banco de dados.
- Pagamento real da Zona Azul.
- Integração oficial com órgãos de trânsito.

### Ambiente de desenvolvimento

O projeto será organizado e desenvolvido no **Visual Studio Code (VS Code)**.

O VS Code será utilizado para:

- organizar os arquivos do projeto;
- editar os conteúdos;
- executar e testar a aplicação;
- visualizar e acompanhar as alterações;
- organizar o projeto para publicação.

**Importante:** o VS Code é o ambiente de desenvolvimento, e não uma linguagem de programação.

A primeira versão será testada pelo navegador. Os dados simulados ficarão separados da parte visual para facilitar futuras alterações.

### Fluxo principal

1. O motorista abre o Safepark antes de sair.
2. Escolhe o destino.
3. Consulta a ocupação e a classificação.
4. Visualiza as regiões mais livres.
5. Decide onde procurar vaga.
6. Ao liberar uma vaga, registra a saída e recebe pontos.
7. Outro motorista pode denunciar o aviso se a vaga continuar ocupada.

---

## 8. Backlog e responsabilidades

| ID | Resultado esperado | Responsável | Apoio/revisão | Previsão |
|---|---|---|---|---|
| T01 | Visão geral e recorte registrados. | [Integrante 1] | [Integrante 2] | 16/11 |
| T02 | RF, RNF, regras e critérios coerentes. | [Integrante 2] | [Integrante 3] | 16/11 |
| T03 | Acesso ao repositório e divisão de tarefas conferidos. | [Integrante 3] | [Integrante 1] | 16/11 |
| T04 | Mapa, destino, ocupação e lista de regiões prontos. | [Integrante 1] | [Integrante 4] | 23/11 |
| T05 | Aviso de saída, pontos e dias grátis prontos. | [Integrante 2] | [Integrante 1] | 23/11 |
| T06 | Denúncia e penalidade prontas. | [Integrante 3] | [Integrante 4] | 23/11 |
| T07 | Dados separados da interface e publicação no GitHub Pages. | [Integrante 4] | [Integrante 2] | 23/11 |

---

## 9. Revisão e contribuições individuais

### Registro da revisão

Descrever uma mudança feita após a revisão do grupo e como ela foi conferida.

### Uso de IA

O grupo utilizou IA como apoio para organizar e revisar o documento a partir da apresentação do Safepark e do modelo de exemplo.

A equipe deve registrar o que foi ajustado manualmente e como conferiu os cálculos e regras.

### Evidências de autoria

| Integrante | Contribuição | Como conferiu | Commit |
|---|---|---|---|
| [Nome 1] / [@usuário] | [Contribuição] | [Como conferiu] | [URL do commit] |
| [Nome 2] / [@usuário] | [Contribuição] | [Como conferiu] | [URL do commit] |
| [Nome 3] / [@usuário] | [Contribuição] | [Como conferiu] | [URL do commit] |
| [Nome 4] / [@usuário] | [Contribuição] | [Como conferiu] | [URL do commit] |

---

## 10. Envio e avaliação

### Repositório

Deixar um documento por equipe com as definições, o planejamento e as evidências.

### Classroom

Enviar os materiais e links dentro do prazo definido pelo professor e conferir o acesso do docente ao repositório e aos commits.

### Apresentação

A equipe deve explicar:

- o problema;
- o usuário;
- o recorte;
- como funciona a v0.1;
- as regras principais;
- o que está dentro e fora do escopo.

Cada integrante deve explicar uma decisão ligada ao usuário e um resultado esperado.

### Valor da etapa

**3,50 pontos**, sendo **1,50 ponto coletivo** e **2,00 pontos individuais**.
