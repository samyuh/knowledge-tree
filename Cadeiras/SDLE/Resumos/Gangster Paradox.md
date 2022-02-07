---
aliases: [Gangster Paradox]
tags: ["#communication"]
---

# Gangster Paradox
## Como coordenar tendo em conta que as mensagens são unreliable? 
→ A1 envia mensagem a dizer que vai atacar
→ A2 responde a dizer que recebeu
→ A1 pode atacar? Não, porque o A2 não sabe se recebeu

Relacionado com o *Three Handshake* do [[TCP]]? 
	Não, porque após a terceira mensagem, o A1 não sabe se o A2 recebeu a mensagem e pode atacar.

Este problema não tem solução, eles nunca vão ter a certeza se vão atacar. Daí o motivo do paradoxo.

## Alternativa
Criar um canal sync e reliable que permite a comunicação entre o A1 e A2.