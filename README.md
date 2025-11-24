# 🤖 TechStudyPlanner — Agente Inteligente de Planos de Estudo

O **TechStudyPlanner** é um agente inteligente desenvolvido para criar **planos de estudo personalizados**, práticos e realistas, com foco em tecnologias como Cloud, Backend, Dados, Mobile, DevOps, Segurança, IA e outras áreas de TI.

Ele organiza cronogramas completos com datas, horários, revisões, checkpoints e envia o plano por e-mail via **Azure Logic Apps**, respeitando as regras definidas pelo Azure Foundry.

---

## 🎯 Objetivo do Projeto

O objetivo é fornecer um agente capaz de:

- Coletar automaticamente informações essenciais do usuário.
- Construir planos de estudo realistas conforme disponibilidade.
- Gerar HTML profissional para e-mail.
- Criar JSON compatível com um **Logic App** que envia o cronograma final ao usuário.
- Seguir regras rígidas de validação de período, disponibilidade, nível e preferências.
- Guiar o usuário até o envio final por e-mail.

---

## 🚀 Funcionalidades Principais

### 🔍 Coleta de Informações
O agente identifica ou solicita os seguintes dados:
- Tecnologia (stack)
- Objetivo final
- Período de estudo
- Disponibilidade (dias/horários)
- Nível atual
- Preferências de conteúdo

Aceita mensagens fragmentadas e reconstrói a intenção.

---

### 📅 Geração do Plano de Estudo
O agente produz:

- Tabela organizada em HTML
- Cronograma dividido por sessões
- Datas e horários reais
- Revisões + checkpoints
- Observações adicionais
- Resumo final em tópicos

---

### 📧 Envio por E-mail
O agente gera um JSON final **compatível com Logic Apps**:

```json
{
  "email_to": "email-do-usuario",
  "email_subject": "Seu Plano de Estudos — <STACK> | <INI> a <FIM> - by TechStudyPlanner",
  "email_body": "<!DOCTYPE html><html lang='pt-BR'> ... HTML completo ... </html>"
}
```


---

## 🚀 Passo a passo para criação do agente TechStudyPlanner no Azure AI Foundry

### 1️⃣ Criação do Grupo de Recursos
![Grupo de recurso](https://drive.google.com/uc?export=view&id=16nkyQIYrKy3ypMP_5Y_M_BGd9kgzaesi)

---

### 2️⃣ Criando o Projeto no Azure AI Foundry
![Criando Projeto](https://drive.google.com/uc?export=view&id=10B3uDFc7jdKGkkyTRQi2vuNkjYot0olN)

---

### 3️⃣ Selecionando o Modelo
![Modelo Selecionado](https://drive.google.com/uc?export=view&id=12BXY9zZNfRtxqVGRjKGgkjNZXscsttML)

---

### 4️⃣ Definindo o Tipo de Implantação

![Tipo de implantação](https://drive.google.com/uc?export=view&id=10KMJteUEHPumk1UarEYqD9tj5TalHlub)

---

### 5️⃣ Configuração do Agente  
Edite o nome, descrição, temperatura, Top P e cole as instruções do agente no campo apropriado:

<details> <summary><strong>📌 Clique para expandir o prompt completo</strong></summary> <br>
Você é o TechStudyPlanner, um agente especialista em criar planos de estudo práticos, realistas e personalizados para tecnologias como Cloud, Backend, Mobile, Data, DevOps, Segurança, IA, etc.
Seu objetivo é gerar cronogramas de estudo completos, formatados e organizados, e produzir um payload JSON pronto para envio por e-mail em HTML, com remetente personalizado.

1️⃣ Coleta obrigatória de informações
Antes de gerar qualquer plano, verifique se o usuário já informou:
- Stack/tecnologia
- Objetivo final
- Período de estudo (datas exatas ou relativo, ex.: “1 semana”)
- Disponibilidade: dias e horários
- Nível atual
- Preferências de conteúdo

★ Aceitar mensagens fragmentadas.
O agente deve reconstruir a intenção mesmo quando as informações chegam em múltiplas mensagens separadas.
Somente pergunte algo se realmente estiver faltando uma informação obrigatória.

2️⃣ Regras sobre período de estudo
- Nunca usar datas no passado.
- Nunca criar sessões fora do período informado.
- Período relativo: início = data atual; fim = data atual + dias.
- Se datas estiverem invertidas ou incoerentes → pedir correção.

3️⃣ Regras para criação do plano
O cronograma deve ser dividido conforme a disponibilidade real do usuário.

Cada sessão deve conter:
- title
- description
- date (YYYY-MM-DD)
- startTime (HH:mm)
- endTime (HH:mm)

Incluir: revisões, checkpoints, exercícios e práticas.

Apresentação obrigatória:
✔ Tabela organizada  
✔ Resumo em tópicos  
✔ Observações/dicas  
✔ JSON para envio por e-mail  

4️⃣ Regras sobre o JSON para envio por e-mail
O agente deve gerar um JSON no seguinte formato:

{
  "email_to": "email-do-usuario",
  "email_subject": "Seu Plano de Estudos - <STACK> | <DATA_INICIO> a <DATA_FIM> - by TechStudyPlanner",
  "email_body": "<!DOCTYPE html><html lang='pt-BR'> ... todo o HTML aqui ... </html>"
}

5️⃣ Corpo HTML do e-mail
Criar:
- Tabela HTML estilizada  
- Resumo  
- Observações  

Usar placeholders:  
{{STACK}}, {{OBJETIVO}}, {{SESSIONS}}, {{OBSERVACOES}}, {{DATA_INICIO}}, {{DATA_FIM}}, etc.

6️⃣ Regras para envio de e-mail
Sempre perguntar:
“Para qual e-mail você deseja enviar o cronograma?”

Depois perguntar:
“Deseja que eu envie esse cronograma para este e-mail agora?”

Só executar a action se o usuário confirmar.

7️⃣ Validações
- Período insuficiente  
- Horários conflitantes  
- Dados faltantes  

8️⃣ Tom da resposta
Profissional, claro, empático e organizado.

9️⃣ Segurança
Nunca pedir senhas.  
Usar somente informações fornecidas.  
Não armazenar dados sensíveis.

</details>

![Configuração do agente](https://drive.google.com/uc?export=view&id=1hS76Ah4vN80MwKlBEmIR8jjZw-bycMVE)

### 6️⃣ Adicionar ação
Seguimos com a configuração da ação em Aplicativos Lógicos da Azure
![ Adicionar ação](https://drive.google.com/uc?export=view&id=16Ab2YDeQMdHN51Ov_BQOuYoRNyHnMaCq)

### 7️⃣ Configuração da ação
![ Configuração da ação](https://drive.google.com/uc?export=view&id=1GhqKrMIjm6yWGfMg4Ll4xWMEPlLiDuK6)

### 8️⃣ Autenticando com o E-mail
Selecione uma conta válida do Office 365 com permissão para envio de e-mails e finalize a configuração.
![Autenticado com E-mail](https://drive.google.com/uc?export=view&id=1Qcy7PbtkWoKY1xkL8yTjL9hS_KB-l_HE)

## 9️⃣ Agente Criado
Após finalizar a configuração, utilizamos o Playground do Azure AI Foundry para conversas e validações do agente.
![Agente Criado](https://drive.google.com/uc?id=1iscwGco2N5lvawKIYc-OT4iT6kYeA8ic)

### 🧪 Prints dos Testes de Prompt

A seguir apresento os testes realizados com o agente para validar sua capacidade de interpretar solicitações, gerar cronogramas personalizados e enviar e-mails automaticamente.

---

## 📌 Teste 1 — Geração do plano de estudos inicial

Enviei a seguinte solicitação ao agente:

> Olá, estou participando do programa **Azure Frontier Girls: Formação e Liderança Feminina na Era Agentic**, uma iniciativa gratuita que capacita mulheres cis e trans para liderarem projetos com agentes de IA e arquiteturas multiagente na plataforma Microsoft Azure, além de promover conexões entre as participantes e sessões de networking com gestores de recrutamento.  
> Quero a certificação **AZ-900**, tenho disponibilidade todas as terças, quartas e sextas das 19h às 21h, com preferência por vídeos e práticas.  
> Solicitei também a inclusão de **dicas de constância** e hábitos para me manter próxima da certificação.  
> O e-mail deveria ser enviado para **estudosm000@gmail.com**.

### 📷 Prints da execução
![Teste Prompt 1](https://drive.google.com/uc?export=view&id=15ggi3W4rf69vISeho2TAuTtK1Hx3-GYR)
![Teste Prompt 2](https://drive.google.com/uc?export=view&id=1kFJPcu7G7B9eaAK7rari9m6vDPqTlaF3)
![Teste Prompt 3](https://drive.google.com/uc?export=view&id=1haAJKicjLjYguxKMXYN2bO6NFqc1tw3I)
![Teste Prompt 4](https://drive.google.com/uc?export=view&id=1Q4vh1sJAANtlWYFXfDdwkkCMQsD0PpAH)

### ✉️ Primeiro e-mail enviado pelo agente
![Email 1](https://drive.google.com/uc?export=view&id=1kicHwA7GoTvHwUjakYxj-VLPzxIre6bJ)

---

## 📌 Teste 2 — Geração de novo cronograma (intensivão de simulados)

Após o envio do primeiro e-mail, iniciei um novo teste na mesma conversa:

> Quero realizar um **intensivão de simulados**, com um novo cronograma contendo **um simulado diário de 16/12/2025 a 23/12/2025**, enviado para um novo endereço de e-mail.

### 📷 Prints da execução
![Teste Prompt 5](https://drive.google.com/uc?export=view&id=1a3m4X8q8CvCb-d49c11yn-kYXJaH0w-R)
![Teste Prompt 6](https://drive.google.com/uc?export=view&id=1wZtrym-QYx3yIYjmtHAzI-O2vd6G5nRq)

### ✉️ Segundo e-mail enviado pelo agente
![Email 2](https://drive.google.com/uc?export=view&id=1udlHKhoopbfr1ZOEoXVFGNWe3bP-e1o1)

---

Esses testes demonstram que o agente é capaz de:
- interpretar instruções complexas,
- gerar planos completos e personalizados,
- adaptar cronogramas conforme novas solicitações,
- e enviar e-mails automaticamente via fluxo integrado.

## 🔗 Referências
- Azure AI Foundry – [https://ai.azure.com/]
- Azure Logic Apps – [https://learn.microsoft.com/pt-br/azure/logic-apps/]
