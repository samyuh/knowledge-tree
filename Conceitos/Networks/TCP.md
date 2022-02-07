---
aliases: [TCP, Transmission Control Protocol]
tags: ["#communication"]
---

# TCP
## Three Handshake
Handshake to TCP TODO

## Reliability
#### Message Loss
→ The application will be notified if the local end is unable to communicate with the remote end
It is up to the application to deal with this

#### Message duplication
→ TCP is not able to filter duplicated data.
For this reason we cannot risk to send duplicated information. There’re some applications, for example, that works with **non-indepotent** operations (e.g credit/debit operations).