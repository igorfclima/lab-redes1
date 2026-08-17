# Respostas

## Parte A — TCP

1. Dá erro na hora, tipo conexão recusada. Faz sentido porque o TCP precisa de alguém escutando na porta pra fechar o handshake antes de trocar qualquer coisa, então sem servidor rodando não tem quem responda o pedido de conexão.
2. Isso é mérito dos números de sequência que cada segmento carrega. O receptor usa esses números pra reorganizar tudo na ordem certa e perceber se algum pedaço se perdeu no caminho antes de entregar pra aplicação.
3. Não suporta, e dá pra ver isso direto no código: o accept só é chamado uma vez, sem laço nenhum em volta. Se um segundo cliente tentar entrar, ele fica esperando pra sempre, porque o servidor já fecha o processo assim que termina de atender o primeiro.

## Parte B — UDP

1. Nada acontece na hora, o que é meio contraintuitivo. O envio simplesmente joga o datagrama na rede sem checar se tem alguém do outro lado, então o cliente fica preso esperando uma resposta que nunca vai chegar. Já no TCP a coisa quebra na hora, no próprio handshake.
2. DNS é um bom exemplo, já que a consulta é rapidinha e se perder o pacote é só mandar de novo. Chamada de voz e vídeo também, porque ali é melhor perder um pedacinho do áudio do que travar tudo esperando retransmissão.
3. Dá pra fazer, sim, guardando o endereço de quem manda cada pacote. O complicado é que o UDP não avisa quando alguém sai, então precisaria ficar mandando mensagens de "ainda tô aqui" de tempos em tempos e definir um prazo pra considerar que a pessoa desconectou.

## Parte C — Multicast

1. Repetir por unicast significa mandar uma cópia inteira do pacote pra cada pessoa, então quanto mais gente, mais tráfego sai do remetente. No multicast o pacote sai uma vez só, e são os próprios roteadores que fazem as cópias, só nos pontos onde os caminhos realmente se separam.
2. O TTL é tipo um contador de fôlego do pacote: cada roteador que ele passa desconta um, e quando chega a zero ele morre ali. Isso evita que um aviso pensado pra rede local acabe se espalhando pela internet inteira.
3. Não recebe, e isso meio que resume a lógica do multicast: não tem histórico guardado em lugar nenhum, é tudo ao vivo. Quem não estava inscrito no grupo na hora do envio simplesmente perdeu aquele aviso.

## Parte D — WebSocket

1. A conexão continua sendo a mesma TCP de sempre, só que a partir do handshake ela para de falar HTTP e os dois lados passam a poder mandar mensagem pro outro a qualquer momento, sem precisar abrir uma requisição nova toda vez.
2. A diferença que mais chamou atenção é quem toma a decisão de pra quem mandar. No multicast quem decide é a rede, através dos roteadores e do IGMP. No WebSocket é o próprio código do servidor que guarda a lista de quem está conectado e manda mensagem um por um.
3. Porque ele já resolve na lata um monte de coisa que a gente teria que inventar na mão usando TCP puro, tipo saber onde uma mensagem termina e outra começa, fechar a conexão direito e manter ela viva. E o detalhe que faz toda diferença pro mural: dá pra usar direto do navegador, coisa que TCP cru simplesmente não permite.
