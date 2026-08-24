# Central de Avisos da Turma — Lab de Redes

Repositório do laboratório de redes 1

## Estrutura

```
lab-redes/
├── java/
│   ├── tcp/
│   ├── udp/
│   ├── multicast/
│   └── websocket/
├── python/
│   ├── tcp/
│   ├── udp/
│   ├── multicast/
│   └── websocket/
├── evidencias/
│   ├── tcp/
│   ├── udp/
│   ├── multicast/
│   └── websocket/
├── RESPOSTAS.md
└── README.md
```

A ferramenta de IA foi utilizada para auxiliar na elaboração do repositório, como em auto-complete, geração da estrutura de diretórios, readme e solucionar duvidas tanto de código quanto de conceitos.

As respostas às questões de cada parte (A, B, C, D) estão em [RESPOSTAS.md](RESPOSTAS.md).

## Lab gRPC — Central de Atendimento da Turma

Continuação do laboratório anterior, agora usando Protocol Buffers e gRPC em vez de sockets manuais.

```
proto/
└── central.proto
java/
└── grpc-central/
    ├── pom.xml
    └── src/main/
        ├── java/br/pucminas/labdamd/central/
        │   ├── ServidorCentral.java
        │   └── ClienteCentral.java
        └── proto/
            └── central.proto
python/
└── grpc_central/
    ├── servidor_central.py
    └── cliente_central.py
evidencias/
├── unario/
└── streaming/
```
