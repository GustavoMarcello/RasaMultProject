# Multi-Chatbots com MultiProjectImporter (Rasa)

<div align="center"><img src = "https://liniribeiro.github.io/assets/posts/rasa/rasa-logo-canva.png" width="200" height="180"><img src = "https://image.freepik.com/vetores-gratis/conjunto-de-robos-bonitinho_74855-6353.jpg" width="200" height="180">
</div>

## Introdução
O Rasa Open Source tem uma lógica incorporada para coletar e carregar dados de treinamento escritos em um modelo próprio. Nesse projeto foi utilizado o MultiProjectImporter, com esse recurso é possível treinar um modelo combinando vários projetos Rasa reutilizáveis.

O MultiProjectImporter é um importador de arquivos com extensões em formato .yml mantendo-os mais organizados, compartilhando os arquivos (Intents, Stories e Responses) entre si.

As vantagens de usar o Multi-Chatbot aparecem quando o chatbot principal contém assuntos diferentes, mas que devem estar juntos para um único sentido. Sabendo que cada assunto tem as suas próprias regras e ramificações. Nesse projeto, foi necessário dividir os assuntos na pasta "projects" abordando um determinado tema com sua tratativa separadamente.

O MultiProjectImporter apesar de ser desenvolvido separadamente, necessita somente de um treinamento, gerando um arquivo unificado de modelo na pasta “models”, isso porque é utilizado apenas uma configuração para o bot como um todo, porém, ainda existe a opção de treiná-los separadamente, fazendo o treinamento apenas dos arquivos “nlu.yml” que estão nas pastas de cada projeto.

## Requisitos
Para instruir o Rasa a usar o MultiProjectImporter módulo, você precisa adicioná-lo à importers lista em sua raiz config.yml.

```  
importers:
- name: MultiProjectImporter
imports:
- projects/Nome_Chatbot_1
- projects/Nome_Chatbot_2
- projects/Affirm_Deny
- projects/Basics
```
Crie um diretório chamado projects na raiz do seu chatbot Rasa, contendo diretórios próprios para cada chatbot que você deseja importar.

Considere a seguinte estrutura de diretórios:

```
.
└── actions
    ├── custom_action_1.py
    └── custom_action_2.py
└── data
    ├── nlu.yml
    ├── rules.yml
    └── stories.yml
└── projects
    ├── Affirm_Deny
    │   ├── data
    │   │   ├── nlu.yml
    │   │   └── stories.yml
    │   └── domain.yml
    ├── Basics
    │   ├── data
    │   │   ├── nlu.yml
    │   │   └── stories.yml
    │   └── domain.yml
    ├── Nome_Chatbot_1
    │   ├── data
    │   │   ├── nlu.yml
    │   │   └── stories.yml
    │   └── domain.yml
    └── Nome_Chatbot_2
        ├── data
        │   ├── nlu.yml
        │   └── stories.yml
        └── domain.yml
├── config.yml
├── credentials.yml
├── domain.yml
└── endpoints.yml
```
## Usabilidade
Depois de estruturar seus diretórios e adicionar os importers e imports em seu config.yml basta adicionar todas as informações de cada “sub-chatbot” em seu respectivo projeto.

Vale notar que tudo o que for global no chatbot, como saudações, despedidas ou regras, continuam nos arquivos raiz do chatbot.

Com a estrutura e informações do chatbot preenchidos, basta treinar fazendo com que o rasa combine todas as informações em um arquivo unificado de treinamento, e utilizar o chatbot normalmente.