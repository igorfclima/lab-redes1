# Respostas

## Parte A — TCP

1. Recusa a conexão, o TCP precisa que alguem esteja escutando.
2. Isso é mérito dos números de sequência que cada segmento carrega.
3. Não suporta, o accept só é chamado 1 vez não a loops.

## Parte B — UDP

1. Nada acontece na hora, o cliente fica esperando infinito, diferente do TCP que trava.
2. DNS é um bom exemplo, já que a consulta é rapidinha e se perder o pacote é só mandar de novo.
3. Possivel sim, guardando o endereço de quem manda cada pacote.

## Parte C — Multicast

1. Repetir por unicast significa mandar uma cópia inteira do pacote pra cada pessoa, então quanto mais gente mais trafego é cosumido.
2. O TTL é tipo um contador de fôlego do pacote cada router equivale a 1 e quando vira 0 ele morre.
3. Não recebe, é como o multicast funciona, é ao vivo.

## Parte D — WebSocket

1. A conexão continua sendo a mesma TCP de sempre, mas agora ambos podem mandar mensagem.
2. A diferença que mais chamou atenção é quem toma a decisão de pra quem mandar. Diferente do multicast que o código decide quem manda e recebe.
3. Porque ele já resolve na lata um monte de coisa que usando TCP iria ter que reinventar a roda.

---

# Lab gRPC — Central de Atendimento da Turma

## Parte A — Transparências em Sistemas Distribuídos

### Tarefa 4.1 — revisão do lab de sockets: TCP, UDP, Multicast e WebSocket

**TCP**

1. Endereço fixo. Prejudica a transparência de localização, porque se o servidor mudar de máquina o cliente quebra.
2. É texto seco que o servidor interpreta na mão. Meio-termo.
3. Ia parar de funcionar, porque o endereço tá fixo.

**UDP**

1. Endereço fixo. Prejudica localização do mesmo jeito.
2. Também texto seco, servidor faz o parsing. Meio-termo.
3. Não sobrevive, mesmo motivo do TCP.

**Multicast**

1. O grupo multicast é fixo no código, mas é um endereço de grupo. Diminui a transparência de localização, mas não tanto.
2. Ainda é texto seco montado e interpretado na mão. Meio-termo.
3. Sobrevive, o cliente escuta o grupo.

**WebSocket**

1. Também fixo. Mesmo problema de localização.
2. Usa JSON, mas ainda é o código na mão. Meio-termo.
3. Mesma coisa dos outros.

### Perguntas — Parte A, seção 4.3

1. A de acesso, porque é diferente, as outras são simples mensagens.

2. Não. Se uma chamada falha e o sistema não conta como sabe que falhou ou se outra pode falhar.

3. TCP exige pensar em rede o gRPC já faz tudo.

## Parte B — Protocol Buffers e o contrato do serviço

1. O código é gerado a partir do proto, cria um padrão na mensagem.

2. O proto é neutro, linguagem é irrelevante.

3. Em Java, a classe CentralAtendimentoGrpc. Em Python, o arquivo central_pb2_grpc.py tem a classe CentralAtendimentoServicer.

## Parte C — RPC unário: ConsultarHorario

1. Serializa a mensagem em bytes no formato protobuf, abre conexão HTTP/2 com o servidor, manda os bytes pela rede e espera a resposta voltar antes de continuar.

2. Antes tinha o código manual de code e decode. Agora é o protobuf e pelo gRPC.

3. Dá erro do tipo UNAVAILABLE, parecido com o TCP recusando a conexão quando não tem cliente.

## Parte D — RPC com streaming de servidor: AcompanharAvisos

1. Precisaria o servidor guardar a lista de clientes conectados e mandar o mesmo aviso pra cada um.

2. Python, é direto ao ponto.

3. O servidor recebe um erro ao tentar mandar o próximo aviso e fecha.

(Sim foi utilizado o o Claude para formato das respostas, mas não para gerar as m esmas)
