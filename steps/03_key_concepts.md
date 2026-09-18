# Conceitos-chave

Nesse workshop, vamos construir uma aplicação usando IA para nos auxiliar no desenvolvimento e deploy. Contudo, recomendo sempre entender os conhecimentos fundamentais por trás do que estamos construindo. Assim, você conseguirá ser crítico sobre o sistema e será mais fácil resolver eventuais problemas.

## Hospedagem de site estático

Um site estático é um conjunto de arquivos prontos (HTML, CSS e JavaScript) que são entregues ao navegador exatamente como estão, sem processamento no servidor. O HTML descreve a estrutura da página, o CSS cuida da aparência e o JavaScript adiciona interatividade. Esses arquivos são os **assets estáticos** da sua aplicação.

Esses assets precisam morar em algum lugar acessível pela internet. Quando alguém abre sua página, o navegador recupera esses arquivos desse local e os executa localmente, na máquina de quem está visitando. 

### Hospedagem de sites na AWS

A AWS oferece mais de uma forma de hospedar um site estático. Neste workshop vamos usar o AWS Amplify, mas vale entender o que existe por baixo dele.

#### AWS Amplify (recomendada)

**O AWS Amplify é um serviço gerenciado para hospedar e publicar aplicações web** de frontend. Você conecta seu repositório de código (ou envia os arquivos), e o Amplify cuida de construir, publicar e servir a página, já com HTTPS, domínio e distribuição global inclusos.

#### Amazon CloudFront + Amazon S3

Por trás dos panos, a hospedagem do Amplify é montada com dois serviços fundamentais da AWS: o Amazon S3 e o Amazon CloudFront.

O **Amazon S3 (Simple Storage Service) é um serviço de armazenamento de objetos**, onde você guarda arquivos em *buckets*. É nele que os seus assets estáticos (HTML, CSS, JavaScript, imagens) ficam armazenados.

O **Amazon CloudFront é uma CDN (Content Delivery Network)**, ou seja, uma rede de servidores distribuídos pelo mundo que guardam cópias em cache dos seus arquivos perto de quem acessa. Isso ajuda a deixar sua página mais rápida por que ao invés de todo visitante buscar o arquivo no bucket original, ele recebe a cópia do ponto mais próximo.

Juntos eles formam o padrão clássico de hospedagem estática na AWS: o **S3 armazena os arquivos e o CloudFront os distribui globalmente com cache e HTTPS**. Essa é exatamente a arquitetura que o Amplify constrói e gerencia por você automaticamente.

## Fundamentos de compute e serverless

A premissa básica dos serviços de compute é que seu código precisa morar em algum lugar que execute ele para que outras pessoas possam usar. Chamamos essa "casa do código" de **servidor**, que nada mais é do que uma máquina muito potente.

**Compute é onde o seu código executável roda** — a capacidade de processamento que recebe uma requisição, executa a lógica do programa e devolve um resultado. Todo código que "faz algo" (calcular, enviar um email, consultar dados) precisa de compute para ser executado.

Tradicionalmente, nós precisamos provisionar, configurar, atualizar e escalar por conta própria, o que consome tempo e esforço no desenvolvimento. 

**Serverless é um modelo em que você executa código sem gerenciar servidores.** Seu código continua sendo executado por um servidor, mas a provedora de nuvem (como a AWS) é quem cuida de provisionar, escalar e manter a infraestrutura, enquanto você só se preocupa com o código. Nesse modelo, você paga apenas pelo que usa, o que muitas vezes significa custo zero quando não há tráfego.

### AWS Lambda: compute serverless na AWS

**O AWS Lambda é o serviço de compute serverless da AWS**: ele executa o seu código em resposta a eventos, sem que você precise provisionar ou gerenciar nenhum servidor. Você envia sua função, e o Lambda se encarrega de rodá-la e escalá-la conforme a demanda.

O funcionamento gira em torno de três conceitos:

- **Ambiente de execução**: o Lambda cria automaticamente um ambiente isolado com o runtime da linguagem escolhida para rodar seu código. Ele sobe quando necessário e desaparece quando ocioso.
- **Trigger (gatilho)**: é o evento que dispara a execução da função, como uma requisição HTTP, um upload de arquivo no S3 ou uma mensagem em uma fila. Sem gatilho, a função fica parada e não gera custo.
- **Handler**: é a função de entrada do seu código, o ponto que o Lambda chama quando o gatilho acontece. Ela recebe os dados do evento, executa a lógica e retorna a resposta.

No nosso portfólio, o Lambda será acionado pelo formulário de contato para processar o envio do email — rodando só quando alguém de fato envia uma mensagem.
