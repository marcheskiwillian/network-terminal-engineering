Deep technical analysis and troubleshooting of terminal and SSH behavior in ISP and NOC environments.

Esse post é focado para quem usa o Termius (https://termius.com/index.html).

Na minha experiência, esse software sempre foi excelente, ainda mais para o meu ambiente de trabalho, que no caso é um NOC de ISP.

Usei o Termius por bastante tempo e sempre gostei muito. Porém, pelo menos no nosso cenário (Windows, Linux e MacOS), tínhamos um problema um tanto chato quando o utilizávamos para acessar nossos equipamentos de rede, principalmente o nosso roteador de borda.

Aqui possuímos um Huawei NE8000 F1A e também vários Huawei 6750. Em ambos, toda vez que precisávamos apagar ou editar uma linha de comando, acontecia o seguinte: a linha simplesmente se quebrava no meio. Isso atrapalhava demais, pois interferia até mesmo no troubleshooting do dia a dia.

https://github.com/user-attachments/assets/6679b359-5629-41de-a87f-bcec69f08910

Isso virou uma verdadeira pedra no sapato. Chegamos ao ponto de até acionar o suporte da equipe do Termius, mas infelizmente não tivemos uma solução.

Na prática, o que eu imaginava inicialmente era que o problema estava relacionado à versão dos equipamentos. Porém, depois de pesquisar um pouco mais, percebi que o problema estava ligado à forma como o terminal negociava a sessão (TTY, largura de terminal e renderização). Por causa disso, o comportamento ficava inconsistente e acabava quebrando as linhas, então passei a considerar isso um tipo de bug.

Depois de muito quebrar a cabeça, testar outros terminais e comparar o comportamento entre eles, decidi retornar ao Termius. Por sorte (ou coincidência 😅), acabei mexendo em uma configuração que, sinceramente, não fazia o menor sentido na hora.

O que fiz foi o seguinte: aqui acessamos todos os nossos hosts via SSH, então, por padrão, eles já eram configurados para ter acesso direto. Ao editar o host, existe também a opção de adicionar Telnet. Resolvi, por curiosidade, ativar essa configuração (mesmo sem utilizar Telnet).

<img width="2012" height="2574" alt="termius bug" src="https://github.com/user-attachments/assets/c531eb63-2868-4d17-82a6-1e3c407a02aa" />

Ao fazer isso no momento da conexão, ele me pediu para escolher manualmente o SSH, e apos isso o problema de quebra de linha simplesmente desapareceu. Desde então, não tivemos mais a quebra de linha em nenhum roteador ou SW 6750 e derivados.

https://github.com/user-attachments/assets/60be9396-b45a-4515-97e7-f8a8eed0866e

Sinceramente, isso para mim não fazia o menor sentido. Porém, pesquisando na internet e com ajuda do ChatGPT, entendi que ao ativar o protocolo Telnet no host o Termius altera a forma como negocia a sessão e a renderização do terminal, o que acaba resolvendo o problema.

Sei que é algo simples, mas decidi compartilhar isso porque talvez existam outros usuários como eu, principalmente profissionais de NOC, que podem estar passando por algo parecido, especialmente em ambientes com equipamentos Huawei e derivados.






