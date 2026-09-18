Agora que seu assistente de IA está conectado a sua conta AWS, vamos usar suas habilidades para fazer o planejamento da aplicação

# Planejando a aplicação com IA

Independente do seu nível de conhecimento atual de arquitetura em nuvem e AWS, podemos usar a IA para fazer planejamento da estrutura e arquitetura da nossa aplicação, aprendendo as melhores práticas de sistemas no processo.

Antes de mais nada, precisamos ter claro o que queremos construir. Para nossa página de portfólio, vamos precisar de:

- Um frontend para o conteúdo estático
- Um backend para a lógica de envio 
- Um serviço que nos auxilie no envio de emails

Vamos usar o Kiro com os poderes importados do Agent Toolkit para planejar a arquitetura. Na CLI do Kiro, cole o seguinte prompt:

> Sou desenvolvedor e quero criar um portfólio pessoal como página web, com conteúdo estático e um formulário de contato no final para receber e-mails. Priorizo simplicidade de deploy e manutenção com deploy contínuo a partir do Git. Quero que a arquitetura fique dentro dos limites da minha conta free tier. Considerando as melhores práticas recomendadas pela documentação oficial da AWS, qual é a melhor arquitetura para minha aplicação? Não crie nada ainda, vamos primeiro planejar.

## A arquitetura

Para esse sistema, recomendo a seguinte arquitetura:
- AWS Amplify para hospedagem da página
- AWS Lambda para lógica backend de envio de emails
- Amazon SNS como serviço auxiliar que fará o envio dos emails

Dado os nossos requisitos, é provavel que o assistente de IA faça recomendações parecidas, mas como os modelos são não determinísticos, podemos ver algumas diferenças. Converse com seu assistente sobre as alternativas para fazer as melhores escolhas.
