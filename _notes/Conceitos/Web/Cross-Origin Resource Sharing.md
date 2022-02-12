---
---

### Same Origin Policy - SOP
Under the policy, a [web browser](https://en.wikipedia.org/wiki/Web_browser_engine "Web browser engine") permits scripts contained in a first web page to access data in a second web page, but only if both web pages have the same _origin_. An origin is defined as a combination of [URI scheme](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier "Uniform Resource Identifier"), [host name](https://en.wikipedia.org/wiki/Hostname "Hostname"), and [port number](https://en.wikipedia.org/wiki/Port_(computer_networking) "Port (computer networking)"). This policy prevents a malicious script on one page from obtaining access to sensitive data on another web page through that page's [Document Object Model](https://en.wikipedia.org/wiki/Document_Object_Model "Document Object Model").

Analogia de um sistema operativo com o browser:
![[web-model-compare.png]]

#### Características do sop
**Confidencialidade**: Dados de uma origem não podem ser acedidos por código de origem diferente.
**Integridade**: Dados de uma origem não podem ser alterados por código com uma origem diferente.

**Origem**:  `host`, `protocol`, `port`

Código numa frame só pode aceder a dados com a mesma origem.
Mais sobre SOP: [How to Understand SOP: Same-origin Policy Whitepaper | Netsparker](https://www.netsparker.com/whitepaper-same-origin-policy/)

#### Pedidos fora do domínio
Uma página/frame pode fazer pedidos HTTP fora do seu domínio
- Escrita geralmente permitida: permite enviar/expor dados a serviços
- Embedding de recursos de outras origens é geralmente permitido

#### Resposta
Os dados contidos na resposta:  
- Podem ser processados nativamente pelo browser (e.g., criar frame)  
- Não podem ser analisados programaticamente (por princípio)  
- O embedding expõe alguma informação

#### Exemplos
-   **HTML**
	-  Não podemos analisar o código programaticamente 
	- Podemos criar frames.
	- Exemplo:  
		- Imagens: não podemos ver quantos pixels uma image tem, mas podemos ver o seu tamanho.
-   **Javascript**
	- Pode ser executado, mas somente no nosso contexto
	- um código de javascript não pode alterar outro javascript de uma origem diferente. Além disso, **não podemos analisar o código programaticamente**.
-   **iframe** 
	- Assim como as imagens, não podemos ler o conteúdo do iframe programaticamente nem um iframe pode aceder os recursos da paǵina que está a exibir. É um sistema isolado. Melhor explicação: [https://security.stackexchange.com/questions/67889/why-do-browsers-enforce-the-same-origin-security-policy-on-iframes](https://security.stackexchange.com/questions/67889/why-do-browsers-enforce-the-same-origin-security-policy-on-iframes)

#### Exemplo de ataque evitado
1. Podemos ser enganados a aceder um website com o seguinte url: [www.badbank.com](http://www.badbank.com) . O website cria um `iframe` do [www.bank.com](http://www.bank.com) . Com isto, podemos pensar que estamos no site legítmo e fazemos login no site.  Desta forma o `badbank` pode recolher nossas informações ou até mesmo enviar requests para o nosso banco.
3.  Same Origin Policy não evita apenas que possamos fazer requests a outros origens cegamente.

Referência: [https://www.netsparker.com/whitepaper-same-origin-policy/#WorldWithoutSameOriginPolicy](https://www.netsparker.com/whitepaper-same-origin-policy/#WorldWithoutSameOriginPolicy)

Tags: #SOP 