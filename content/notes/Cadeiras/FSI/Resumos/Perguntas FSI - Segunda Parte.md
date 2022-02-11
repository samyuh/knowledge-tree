# Segurança Web: Modelo
1. O que é o SOP? Quais são as limitações que este impõe para HTTP, HTML e Javascript?
	- Resposta: SOP (Same Origin Policy) é uma política de proteção. Sempre podemos escrever pedidos HTTP. O conteúdo escrito na resposta não pode ser visualizado programaticamente, no entanto pode ser processado. Para o HTML e Javascript temos a mesma coisa: podemos ler e executar o conteúdo, mas não podemos analisá-lo programaticamente.

2. O que é considerado um recurso da mesma origem?
	- Resposta: Tem de possuir o mesmo esquema, nome de domínio e porta.

3.  A CIA são conceitos de segurança usados amplamente, a fim de identificar as o tipos de segurança que um recurso define. A SOP possui aplica quais destes conceitos?
	- Resposta: SOP tenta garantir confidencialidade (pelo que não é possível analisar programaticamente dados vindo de outras origens). Também garante integridade, pelo que não é possível alterar dados vindos de outras origens.

4. O que é o CORS?
	- Resposta: É o cross-origin resource sharing. Permite relaxar as políticas do SOP por meio da abertura de algumas exceções à política.

5. O que são pedidos pre-flight?
	- Resposta: É um dummy request feito, a fim de estabelecer a comunicação. Um cliente (lado A) envia este dummy request ao (lado B) e este envia uma resposta permitindo o acesso ou negando-o.

6. Qual a definição de origem para um cookie?
	- Resposta: É apenas o domínio e path. Ou seja, enquanto o URL tem o esquema, domínio e porta, o cookie tem o domínio e path.

7. O SOP permite com que o browser envie cookies para quais domínios?
	- Resposta: Um cookie pode ser enviado se a cookie for um sufixo do domínio da url **e** se a path da cookie for um prefixo da path da URL.
	
8. Explique o SameSite=Strict e SameSite=Lax?

9. Como podemos evitar que um cookie seja lido por javascript?
	- Resposta: Colocando a flag HTTPOnly=true
	
10. Por quê utilizar (i)frame?

11. Complete o esquema abaixo:
![[web-model-cookies-empty.png]]

# Segurança Web: Ataques
1. O que é CSRF? Cite um exemplo e medidas para impedí-lo.
	-  Um CSRF é um cross site request forgery. Acontece quando o atacante faz com que o utilizador faça um request a um website a partir de uma fonte suspeita. Um caso comum é o user ter salvo no browser um cookie de sessão para um website específico e, ao clicar numa image, por exemplo, que possui um request a outro website (cujo o utilizador possui sessão iniciada), o request poderá ser aplicado. Uma das formas de impedir o CSRF é adicionar secret tokens juntos a formulários, impedir requests a partir de outras origens, etc.

2. O que é um SQL injection e como podemos previní-lo?
	- O **SQLi** é quando o atacante consegue mudar operações na database a partir do seu input. Pode-se previní-lo realizando queries parametrizadas (não permitem alterações já que são pré-compiladas) e o uso de bibliotecas **ORM** que abstraem o uso da base de dados e o uso de queries. No entanto, a próprias bibliotecas **ORM** podem estar sujeitas a vulnerabilidades.

3. O que é uma parameterized query?
	- São queries pré-compiladas onde são apenas fornecidos os parâmetros dos users. Estas queries não podem ser alteradas já que são pré-compiladas.

4. O que são bibliotecas ORM?
	- São biliotecas que abstraem o uso de base de dados.

5. O que é XSS? Qual a diferença de um reflected XSS para um stored XSS?
	- É Cross Site Script. O utilizador consegue criar um script que é executado pelo website. O reflected XSS não é guardado pela base de dados. Alguem pode clicar num link que contém um script o qual envia a cookie do user para outro website. O stored XSS acontece quando o atacante consegue guardar o script na base de dados do website e quando o administrador. Um exemplo disto é o Samy Worm, que guardou um código html no perfil.

6. Quais são as medidas atuais para a prevenção de um XSS?
	- Podemos evitar o XSS utilizando a content security policy, em que:
		-   Scripts inline não são executados
		-   Apenas scripts de white-list são aceitos
		-   Podemos adicionar ainda opção em que o site não pode ser framed.
	O que ainda pode acontecer é uma source da whitelist ser comprometida. Então podemos adicionar a hash do que se esta esperando receber. Assim se a source for alterada, a flag será mudada.
	
# Criptografia - Parte 1
1. O que é o one-time-pad? Qual o problema dele?
	-   Resposta: O one-time-pad é simplismente gerarmos uma chave qualquer com o mesmo tamanho do texto a ser enviado. O problema é que a chave é apenas usada uma vez e para textos grandes, criar uma chave aleatória é um processo muito lento.
    
2. Qual a solução que se achou para o one-time-pad?
	-   Resposta: Pode-se usar o PRG (pseudo random generator) onde, dado uma key, consegue-se gerar a sequência de bytes para realizar o xor. O problema é que se não for dado um nonce o valor é sempre o mesmo.
    
3. Por que utilizamos nonce?
	-   Resposta: O xor possui a seguinte propriedade m1 xor k = c1 e m2 xor k = c2, então c2 xor c1 == m1 xor m2. Se não usarmos um nonce a confidencialidade por ser comprometida.
    
4. O que torna as cifras de bloco AES atualmente tão populares?
	-   Resposta: A implementação é suportada a nível de hardware.
    
5. Por que é inseguro usar a mesma cifra de bloco para cifrar um plain-text inteiro? Explique a situação com um exemplo.
	-   Resposta: Um exemplo é o Eletronic Code Book (ECB). Ao cifrarmos, por exemplo, uma imagem com a mesma cifra de bloco, temos que as mesmas cores irão ter os mesmos padrões. Com isto no fim é possível identificar e interpretar uma imagem cifrada desta forma (slide 19).
    
6. Cite duas cifras de bloco consideradas seguras.
	-   Resposta: Cipher block chain e Counter Mode.

# Criptografia - Parte 2
1.  No que consiste o protocolo MAC? Quais são as suas garantias?
	-   Resposta: O MAC (Message Authenticate Code) é um protocolo que garante **autenticidade** e **integridade** de mensagens. Quando um computador (**A**) deseja enviar uma mensagem a outro (**B**), deseja-se que **B** tenha certeza de a mensagem recebida foi enviada por **A**. Para isto, **A** envia a mensagem junto com uma **tag,** gerada a partir de uma chave e da mensagem $t = mac(k,m)$. A chave de **A** é pré partilhada com **B** e quando **B** recebe a mensagem ele calcula uma tag $t'$ da mesma forma que **A.** Se for concretizado que $t' = t$, então podemos dizer que a mensagem veio de **A.**
    

2.  Explique as diferenças entre SSH, SSL e IPSEC.
	-   Resposta: Os três são protocolos que tentam garantir os princípios de autenticidade, integridade e ainda confidencialidade. SSH → $m' = [enc(m,k_{enc})|| mac(m,k_{mac})]$ SSL → $m' = [mac(enc(m,k_{enc}),k_{mac}]$ IPSEC → $x = enc(m,k_{enc}) \rightarrow m' = [x || mac(x,k_{mac})]$

3.  O que é AEAD? Como ele é utilizado?
	-   Resposta: É uma maneira de juntar MAC e Cifras. `Enc(m,n,k,data) → (c,t)` `Dec(c,t,k,n)`
    
4.  Qual é uma boa heurística para conseguir aleatoriedade num computador? Qual a sua desvantagem?
	-   Resposta: A aleatoriedade pode ser obtida por meio da avaliação de recursos computacionais (e.g temperatura, uso do processador). O problema desta abordagem reside no facto de que obter estes valores é um processo lento e a entropia aumenta gradualemente com o tempo, ou seja, se for requisitado a obtenção destes valores constantemente pode-se perder um certo grau de aleatoriedade.
    
5.  Compare `random` com `urandom` . Qual dos dois é mais recomendado? Por que?
	-   Resposta: `random`e `urandom` são dois ficheiros no sistema linux capazes de gerar valores aleatórios a partir de medidas de recursos computacionais (uma heurística). O `random` bloqueia até que uma certa entropia seja adquirida. `urandom` por outro lado retorna independente da entropia. Entre os dois ficheiros o `urandom` é o mais recomendado, pois não se sabe muito bem o quão bem o computador consegue dizer se uma entropia é “boa” ou “não”. Ainda, muitas vezes nas aplicações atuais não se lida com o facto de que `random` retorna nada se uma determinada entropia não é atingida e por isso acaba-se por não realizar nenhum tipo de aleatoriedade na encriptografia. Portanto, o `random` além de se correr o risco de deixar o sistema mais lento devido a espera dos níveis de entropia serem satisfatórios, pode ocorrer da aplicação na verdade não gerar nenhuma aleatoriedade para cifrar o conteúdo. Neste sentido, mais vale ter pouca aleatoriedade do que não ter nenhuma.
    
6.  O que é cookie poisoning? Cite um exemplo.
	-   Resposta: Cookie poisoning consiste em alterar a cookie de forma que quando o servidor requisitá-lo a informação obtida seja a que o atacante deseja. Imagine que o atacante é um jogador de jogo. O servidor para envia cookies para os clientes para evitar com que toda a informação seja armazenada nele. Um cookie em particular armazena os pontos de um jogador. Ao alterar a sua informação nesta cookie (i.e quantos pontos o jogador tem), quando o servidor requisitar o cookie novamente a informação implantada pelo jogador será considerada e processada pelo servidor.
# Criptografia - Parte 3

1.  O que é o KDC? Como o KDC faz com que duas outras máquinas possam estabelecer um comunicação segura?
	-   Resposta: É uma máquina central que possui chaves pré-definidas com outras máquinas. Este componente central estabelece a comunicação entre outras duas máquinas conectadas a ela. Imagine que **Alice** e **Bob** queiram falar entre si. Ambos possuem chaves pré partilhadas com o KDC. O KDC usa a sua comunicação segura para enviar a chave simétrica para a comunicação entre **Bob** e **Alice.**
    

2. Quais são as limitações das chaves simétricas? Explique.
	-   Resposta: As chaves simétricas não garantem autenticidade e integridade, já que não há nenhum tipo de confirmação sobre quem enviou a mensagem. ~~Além disso precisam ser pré-partilhadas.~~ Além disso, não garantem o não repúdio. O não repúdio consiste em provar para uma third-party (C) de que a mensagem foi enviada por uma certa pessoa (A). No entanto, (C) pode alegar que já que (B) conhece o conteúdo da mensagem, porque possui a key, (B) poderia ter alterado o conteúdo.
    

3.  ****Como podemos utilizar chaves públicas para transmitir a chave da cifra simétrica? Porque este tipo de comunicação não garante autenticidade?
	-   Resposta: Imagine que **Alice** (A) deseja estabelecer uma comunicação com **Bob** (B) e enviar uma chave simétrica para este. **A** vai encriptar a mensagem com a chave pública de **B** e como apenas **B** possui a chave privada, apenas ele consegue desencriptar o conteúdo. A chave pública é disponível para qualquer um e por isso este de comunicação não garante autenticidade: há ainda a possibilidade de haver um man-in-the-middle na comunicação **Bob** e **Alice.**
    

4.  O que é o paradigma híbrido?
	-   Resposta: O paradigma híbrido é uso em conjunto de chaves públicas e privadas para transferir chaves simétricas.
    
5.  Explique a assinatura digital. Quais são as suas garantias?
	-   Resposta: As assinaturas digitais garantem autenticidade e integridade. Temos dois tipos de chaves em assinaturas digitais: chaves de verificação e chaves de assinatura. As chaves de verificação são públicas e chaves de assinatura são privadas. Quando um agente assina uma mensagem, outras pessoas podem verificar a assinatura. Não é possível alterar o conteúdo da mensagem sem alterar a assinatura.
    

6.  Explique a analogia do envelope. Como esta analogia explica o não repúdio de assinaturas digitais?
	-   Resposta: A analogia do envelope serve para explicar o porquê de ser necessário fazer primeiramente a assinatura e só então a encriptação. A analogia explica que se primeiro encriptamos a mensagem e só depois assinamos é a mesma coisa de assinarmos um envelope lacrado sem saber o seu conteúdo. Encriptar e depois assinar permite que alguem alegue que assinou uma mensagem sem saber o seu conteúdo.

7.  Atualmente “garantimos” ou alegamos que as assinaturas manuais possuem algumas propriedades. As assinaturas digitais procuram garantir estas mesmas. Quais são?
	-   Resposta: Não repudiável Não falsificável Não reutilizável
    
8.  Quais são as vantagens de se utilizar assinaturas digitais e não MACs?
	-   Resposta: Não necessitam chave pré partilhada Garantem o não repúdio
    
9.  Por que MAC não garante o não repúdio?
	-   Resposta: Ver questão 2.

# Criptografia - Parte 4
1.  No paradígma híbrido, devemos encriptar e assinar ou o contrário? Por que?
	-   Resposta: Devemos fazer o sign-then-encrypt. Porque se fizermos encrypt-then-sign a pessoa que assinou determinado conteúdo pode alegar que não sabia o que estava nele, já que estava encriptado. Desta forma perde-se a propriedade de não repúdio.
    

2. O que é perfect forward secrecy? Por que garantir isto é importante?
	- Resposta: É um sistema em que a chave de encriptação é automaticamente modificada a cada encriptação. Desta forma se uma chave for comprometida garantimos que as informações anteriores não são igualmente expostas. Por exemplo, um hacker pode escutar a rede e guardar o histórico de mensagens de um chat. Quando uma chave é comprometida o histórico não é revelado.
    
3.  Explique Diffie Hellman.
	-   Resposta
	    ##### Protocolo vulnerável ao man-in-the-middle
	    **Alice** (A) tem um um número primo $g$ (público) e eleva este número a um fator $x.$ Assim, $g^x= X$. Quando (A) quiser uma comunicação com **Bob** (B), (A) irá enviar $X$ (que muda a cada sessão). (B), por sua vez irá calcular $g^y=Y$, irá enviar $Y$ para (A) e irá computar $X^y = g^{xy}$. (A) por sua vez irá calcular $Y^x = g^{xy}$ e este novo $g^{xy}$ irá ser utilizado como chave.

	    O problema deste protocolo é que este é vulnerável ao man-in-the-middle.
	    
	    ##### Protocolo seguro
	    **Alice** (A) irá enviar $X$ como anteriormente referido. No entanto a resposta de (B) irá conter uma assinatura. $Y, sig(sk_b, Y)$ e depois se (A) confirmar os dados enviará uma resposta $X, sig(sk_a, X)$. Se os dados de (A) se confirmarem a conexão é estabelecida.
    
4.  Como Diffie-Hellman pode evitar o ataque de man-in-the-middle?
	-   Resposta: Pode ser evitado com o uso de assinaturas digitais.

# Public Key Infrastructure
1.  Por que foi criada a PKI?
	-   Resposta: Devido a necessidade de sabermos se a chave de uma pessoa pertence a quem achamos que pertence.
    
2.  O que é uma TTP? Explique uma solução trivial para o problema da autenticidade de chaves. Qual o problema da solução trivial?

	-   Resposta: A TTP (trusted thirdy party) é uma thirdy party que garante que a chave pública de um sujeito realmente pertence a ele. Uma solução trivial para o problema da autenticidade de chaves é termos uma thirdy party (TTP) em que, quando (A) envia uma mensagem assinada para (B) junto a sua key, podemos contactar a TTP e verificar com esta se a chave recebida realmente pertence a (B). O **problema** desta abordagem é que isto forçaria a TTP sempre estar online e a existencia de uma TTP singular não é factível. Além disso outro problema surge: como sabemos que podemos confiar na TTP?
    
3.  Como CA’s amenizam os problemas da questão anterior? Justifique explicando como CAs funcionam.
	-   Resposta: Na questão anterior 3 problemas foram citados: a TTP precisa sempre estar online, não sabemos se podemos confiar na TTP e uma thirdy party singular não é factível. As CAs (certificate authority) são certificados de autoridades responsáveis por verificar se um um certificado digital é válido (estas assinam estes). Quando a CA assina um certificado ela afirma que este é verdadeiro e portanto, a chave que veio junto pertence a quem se espera falar. Isto resolve dois problemas citados anteriormente: a thirdy party não precisa estar sempre online e também podem haver vários CAs. A resolução do problema de confiança é “solucionado” por meio da confiança implicitas em entidades poderosas como a microsoft ou a google. Alguns certificados (os de raíz) são instalados no nosso sistema operacional. Estes certificados de raíz podem assinar outros CAs que assinam outros e assim em diante criando uma cadeia de confiança. É necessário verificar a autenticidade desta cadeia de segurança até que cheguemos num ponto em que conhecemos o certificado que assinou um prévio.
    
4. O que é TSL?
	-   Resposta: É uma trusted service provider list. É uma white list de certificados atualizadas.
    
5.  O que é Online Certificate Status Protocol (OCSP). Qual o problema do seu uso?
	-   Resposta: Pode acontecer ainda de uma CA ser revogada ou um certificado digital ser revogado. Para verificarmos a condição de um certificado, podemos utilizar o Certifica Status Protocol. No entanto, com isto voltamos ao nosso problema inicial de precisarmos ter uma TTP sempre online. O OCSP verifica o estado de revogação de um certificado.
    
6. O que é certificate pinning?
	-   Resposta: É uma técnica obsoleta para restringir certificados permitidos num website. Era enviado para o cliente uma lista de hashed public keys no header do protocolo HTTP. Estas hashed public keys deveriam estar presentes na chain de certificados digitais em conexões futuras.
    
7.  Como é que um utilizador contacta/toma conhecimento de uma CA?
    
8.  Como é que o Bob verifica a assinatura produzida por uma CA num certificado?
    
9.  Como é que o Bob sabe se pode confiar na CA?
    
10.  Como é que os certificados de chave pública circulam/são distribuídos e armazenados?
    -   Resposta: Certificados são armazenados em repositórios e são distribuídos por meio de protocolos seguros como HTTP, MIME, FTP.
    
11.  Qual a diferença entre RA e CA?
	-   Resposta: Uma RA (registration authority) é uma entidade responsável por validar registos e possui contacto direto com o cliente. A Certificate Authority valida um certificado, mas por sua vez não possui contacto direto com o cliente.
    
12.  O que é uma CRL? Como é que sabemos onde está a CRL mais recente? Qual o problema desta abordagem?
	-   Resposta: O CRL é a certificate revogation list. Os próprios certificados geralmente vem com um URL que contém a lista. O problema desta abordagem é que muitas aplicações não suportam esta abordagem.
    
13.  O que são políticas de certificação?
	-   Resposta: É quando uma PKI passa a ter um valor legal. Quando isto acontece, esta recebe uma Object Identifier (OID). A política de certificação geralmente promove direitos e responsabilidaes tanto por parte do consumidor tanto para a CAs. O uso da PKI que fujam do que foi descrito são consideradas ilegalidades, crime.
# Autentication - Parte 1
1.  Diga porque razão é preciso soluções diferentes para a autenticação de origem de mensagens e de entidades.
2.  Qual a solução criptográfica usada para autenticação de entidades? Explique-a.
3.  Como é feita a autenticação de utilizadores humanos?
4.  O que é phishing?
5.  Enumere possíveis ataques a passwords.
6.  É suficiente armazenar a hash em vez da password original?
7.  Como se pode tornar mais difícil ataques por dicionário?

# Segurança de Redes: Parte 1
1.  Localmente como sabemos os endereços MAC de um dos outros?
2.  Como outros routers sabem para onde enviar os pacotes?
3.  Como é feito o handshake de comunicações TCP?

# TLS
1.  Por que não usar HTTPS para todo o tráfego?
2.  Como é feita a ligação do Diffie-Hellman autenticado.