---
title: ! "O Protocolo Maker: Sistema Multi-Collateral Dai (MCD) da MakerDAO"
---

# **Resumo**

O Protocolo Maker, também chamado de sistema Multi-Collateral Dai (MCD), permite que o usuário gere Dai fazendo uso de ativos de garantia aprovados pela “Governança Maker”. A Governança Maker é o processo organizado e conduzido pela comunidade que gerencia os diversos aspectos do Protocolo Maker. O Dai é uma criptomoeda<sup> </sup>com garantia, independente e descentralizada que é indexada pelo dólar americano em um regime cambial intermediário chamado de soft-peg. Resiliente diante da hiperinflação devido à sua baixa volatilidade, o Dai oferece oportunidade e liberdade econômica para todos, onde quer que estejam. 

Este informe técnico é uma descrição de fácil leitura do Protocolo, que foi elaborado com base na blockchain Ethereum. Para usuários com experiência técnica, é possível obter uma explicação mais detalhada de todo o sistema acessando o documento [Introduction to the Maker Protocol](https://docs.makerdao.com/), no Maker Documentation Portal.

[[observação]]
|<span class="note-heading">Sobre o MakerDAO</span>
|O MakerDAO é um projeto de código aberto de blockchain no Ethereum e também uma Organização Autônoma Descentralizada[^1] criada em 2014. O projeto é gerenciado por várias pessoas em diferentes partes do mundo que detêm o token de governança, chamado de MKR. Por meio de um sistema de [governança científica](https://community-development.makerdao.com/governance/governance-risk-framework/part-one) que inclui Votações executivas e Votações de governança, os titulares do MKR gerenciam o Protocolo Maker e os riscos financeiros do Dai para garantir estabilidade, transparência e eficiência. O peso dos votos de MKR é proporcional ao valor de MKR que o membro votante bloqueia no contrato de votação, o DSChief. Ou seja, quanto mais tokens MKR o membro votante tem bloqueados no contrato, maior é o seu poder de decisão.
|
|<span class="note-heading">Sobre o Protocolo Maker</span>
|Construído com base na blockchain Ethereum[^2], o Protocolo Maker permite que seus usuários criem moedas. Os elementos atuais do Protocolo Maker são a stablecoin Dai, os Cofres de Garantias Maker, os Oráculos e as Votações. O MakerDAO regula o Protocolo Maker ao decidir sobre parâmetros fundamentais (por exemplo, taxas de estabilidade, taxas/tipos de garantia, etc.) por meio do poder de votação dos titulares de MKR.
|
|Uma das maiores aplicações descentralizadas (dapps, na sigla em inglês) do blockchain Ethereum, o Protocolo Maker foi a primeira aplicação financeira descentralizada (DeFi) a ser amplamente adotada.  
|
|<span class="note-heading">Sobre a Fundação Maker</span>
|A [Fundação Maker](https://makerdao.com/en/team), parte da comunidade Maker, desenvolveu e lançou o Protocolo Maker juntamente com diversos outros parceiros externos. No momento, ela está trabalhando com a comunidade MakerDAO para autofinanciar a governança descentralizada do projeto e viabilizar sua total descentralização.
|
|<span class="note-heading">Sobre a Fundação Dai</span>
|Com sede na Dinamarca, a Fundação Dai é autogovernada e independente da Fundação Maker. Ela foi criada para armazenar os ativos intangíveis principais da comunidade Maker, como marcas registradas e direitos autorais sobre códigos. Sua operação baseia-se totalmente em estatutos rígidos e objetivos que definem seus mandatos. Como consta do [Contrato fiduciário da Fundação Dai](https://forum.makerdao.com/t/announcing-the-dai-foundation/1046), seu propósito é resguardar aquilo que não é passível de descentralização tecnológica no Protocolo Maker.

# **Introdução**

Iniciado em 2015, o projeto MakerDAO foi desenvolvido a partir da colaboração de desenvolvedores de diversas partes do mundo, trabalhando juntos nas primeiras iterações de código, arquitetura e documentação. Em dezembro de 2017, o primeiro [informe técnico formal do MakerDAO](https://makerdao.com/whitepaper/sai) foi publicado, apresentando o Sistema da stablecoin Dai original (hoje, chamado de Sai). 

Esse documento descrevia como as pessoas podiam gerar Dai utilizando aquele sistema fazendo uso do Ethereum (ETH) como garantia por meio de 
<span class="annotated">contratos inteligentes<span class="annotation">Esses contratos inteligentes são programas de computador que executam ações e regras específicas em uma rede. São basicamente notas promissórias que respondem a códigos de programação, e não a autoridades centrais.</span></span> 
exclusivos conhecidos como Posições de Dívidas com Garantia (CDPs). Como o ETH era o único ativo de garantia aceito pelo sistema, o Dai gerado era chamado de Dai de garantia única (SCD) ou Sai. O informe técnico também inclui um plano de atualização do sistema para torná-lo compatível com ativos com diversas garantias, além do ETH. O que era uma meta passou a ser realidade em novembro de 2019.

O Protocolo Maker (antigo Sistema Stablecoin Dai) aceita como garantia qualquer ativo baseado em Ethereum que tenha sido aprovado pelos titulares de MKR. São eles, aliás, que também votam nos Parâmetros de risco correspondentes a cada ativo de garantia. É importante destacar que as votações são um componente fundamental do processo de governança descentralizada do Maker.

Sejam bem-vindos ao **Sistema Multi-Collateral Dai (MCD)**.


## **Nós Confiamos no MCD**

A tecnologia blockchain cria uma oportunidade inédita de reduzir a frustração e a desconfiança crescentes do público com os disfuncionais sistemas financeiros centralizados. Ao distribuir dados por toda uma rede de computadores, a tecnologia permite que grupos de indivíduos adotem a transparência em vez do controle de uma entidade central. O resultado é um sistema independente, altamente eficiente, transparente e que não requer permissões; um sistema capaz de aprimorar as estruturas monetárias e financeiras globais atuais, além de melhor servir o interesse comum. 

O Bitcoin foi criado tendo esse objetivo. Apesar de bem-sucedido como criptomoeda em diversos aspectos, o Bitcoin não é ideal como meio de troca, pois sua oferta fixa e natureza especulativa geram volatilidade, o que impede a sua difusão como moeda corrente. 

Por outro lado, a stablecoin Dai é bem-sucedida exatamente onde o Bitcoin falhou, já que o Dai foi desenvolvido para _reduzir a volatilidade_ _de preços._ Indexado ao dólar em um regime cambial intermediário,<sup> </sup>o Dai é uma criptomoeda com garantia, independente e descentralizada.  

Desde o lançamento do Dai de garantia única em 2017, [a adoção da stablecoin pelos usuários aumentou drasticamente](https://blog.makerdao.com/dai-in-numbers-momentum-report-q3/), e ela se tornou peça fundamental de aplicações descentralizadas que ajudam na expansão do movimento DeFi (finanças descentralizadas). O sucesso do Dai é parte de um movimento mais amplo do setor que favorece as stablecoins, que foram desenvolvidas para manterem a precificação baseada no valor e funcionarem como dinheiro. 

Por exemplo, em fevereiro de 2019, o JPMorgan se tornou o primeiro banco dos Estados Unidos a criar e testar uma moeda digital que equivale a 1 USD.[^3]  Com o crescimento do setor de criptomoedas, outros bancos, empresas de serviços financeiros e até mesmo governos criarão moedas digitais estáveis (por exemplo, Moedas Digitais de Banco Central), assim como organizações fora do setor financeiro. O Facebook, por exemplo, anunciou planos para a criação da Libra, “uma criptomoeda digital estável que será totalmente garantida por uma reserva de ativos reais”,[^4] em junho de 2019. Contudo, essas propostas comprometem a proposta de valor fundamental da tecnologia blockchain: a adoção global de uma infraestrutura comum sem uma autoridade ou administrador central capaz de utilizar sua influência de modo abusivo.


# **Visão geral do Protocolo Maker e seus recursos**


## **O Protocolo Maker**

O Protocolo Maker é uma das maiores aplicações descentralizadas na blockchain Ethereum. Projetado por um grupo heterogêneo de colaboradores, inclusive desenvolvedores da Fundação Maker, parceiros externos e outras pessoas e entidades, ele foi a primeira aplicação financeira descentralizada (DeFi) a ser amplamente adotada. 

O Protocolo Maker é gerenciado por pessoas do mundo inteiro que detêm o token de governança, chamado de MKR. Por meio de um sistema de [governança científica](https://community-development.makerdao.com/governance/governance-risk-framework/part-one) que envolve Votações executivas e Votações de governança, os titulares de MKR gerenciam o Protocolo e os riscos financeiros do Dai para garantir estabilidade, transparência e eficiência. Um token MKR bloqueado em um 
<span class="annotated">contrato de votação<span class="annotation">O contrato de votação assegura que os titulares de MKR possam votar com o valor total do MKR correspondente a participação deles.</span></span>
equivale a um voto.


## **A stablecoin Dai**

O Dai é uma stablecoin com garantia, independente e descentralizada<sup> </sup>que é indexada ao dólar em um regime cambial intermediário. Ele é mantido em 
<span class="annotated">carteiras de criptomoedas<span class="annotation">Uma carteira de criptomoedas é uma ferramenta utilizada para gerenciar ativos de criptomoedas e interagir com aplicações descentralizadas (dapps). Na carteira de criptomoedas, o usuário consegue visualizar uma lista de suas moedas e tokens, seus saldos e histórico de transações, além de realizar transferências.</span></span>
ou em plataformas, sendo compatível com Ethereum e outras blockchains conhecidas. 

O Dai é fácil de gerar, acessar e usar. O usuário gera Dai ao depositar ativos de garantia em 
<span class="annotated">Maker Vaults<span class="annotation">Esses Maker Vaults viabilizam a geração de Dai mediante garantias bloqueadas. O usuário pode abrir seus cofres por meio do painel Oasis Borrow ou de outras diversas interfaces que permitem o gerenciamento de operações com Cofres.</span></span>
no Protocolo Maker. É assim que o Dai entra em circulação e o usuário ganha liquidez. Também é possível comprar Dai de corretoras e casas de câmbio ou, ainda, receber a moeda como forma de pagamento. 

Depois de gerado, comprado ou recebido, o Dai pode ser usado da mesma forma que qualquer outra criptomoeda: pode ser enviado para outras pessoas, usado como pagamento para bens e serviços ou, até mesmo, guardado como poupança por meio de um recurso do Protocolo Maker denominado 
<span class="annotated">Taxa de poupança do Dai (DSR, na sigla em inglês)<span class="annotation">A Taxa de poupança do Dai (DSR) permite que todos os titulares de Dai gerem poupança de forma nativa e automática ao bloquear seu Dai em um contrato DSR. A DSR amplia as possibilidades para titulares de Dai, entre eles negociadores de criptomoedas, startups e empresas consolidadas.</span></span>
(DSR). 

Todo Dai em circulação apresenta garantia em excesso, o que significa que o valor da garantia é maior do que o valor da dívida em Dai. Além disso, todas as transações em Dai são exibidas publicamente na blockchain Ethereum.


### **Que propriedades do Dai são parecidas com as do dinheiro?**

Em geral, o dinheiro apresenta quatro funções: 



1. Reserva de valor
2. Meio de troca
3. Unidade de conta
4. Padrão de diferimento do pagamento

O Dai tem propriedades e casos de uso projetados para desempenhar essas funções.


#### Dai como reserva de valor

Reserva de valor é todo ativo cujo valor é mantido sem depreciação significativa ao longo do tempo. Como o Dai é uma stablecoin, ele foi desenvolvido para operar como uma reserva de valor mesmo em um mercado volátil. 


#### Dai como meio de troca

Meio de troca é tudo aquilo que representa um padrão de valor e é usado para viabilizar a compra, venda ou troca (negociação) de bens e serviços. A stablecoin Dai é utilizada no mundo inteiro para todos os tipos de fins transacionais.  


#### Dai como unidade de conta

Unidade de conta é uma medida padronizada de valor usada para precificar bens e serviços (por exemplo, USD, EUR, BRL). No momento, o preço de referência do Dai é de 1 USD (1 Dai = 1 USD). Embora o Dai não seja usado como medida padrão de valor no mundo externo à blockchain, ele funciona como unidade de conta no Protocolo Maker e em alguns dapps de blockchain, nos quais a contabilidade ou a precificação dos serviços dos dapps pelo Protocolo Maker estão em Dai, e não em uma moeda fiduciária, como o dólar norte-americano. 


#### Dai como padrão de diferimento do pagamento

O Dai é usado para saldar dívidas no Protocolo Maker. Por exemplo, é possível usar o Dai para pagar a taxa de estabilidade e fechar o cofre. Essa vantagem distingue o Dai de outras stablecoins.


### **Ativos de garantia**

O Dai é gerado, garantido e mantido estável por meio de ativos de garantia depositados em Maker Vaults no Protocolo Maker. Ativo de garantia é um ativo digital que os titulares de MKR aceitaram no Protocolo por meio de votação. 

Para gerar Dai, o Protocolo Maker aceita como garantia qualquer ativo baseado em Ethereum que tenha sido aprovado pelos titulares de MKR. Os titulares também precisam aprovar Parâmetros de risco correspondentes específicos para cada garantia aceita. Por exemplo, ativos mais estáveis podem receber Parâmetros de risco mais lenientes, enquanto ativos mais arriscados recebem Parâmetros de risco mais severos. Abaixo, confira informações detalhadas sobre Parâmetros de risco. Essas e outras decisões são tomadas por titulares de MKR por meio do processo de governança descentralizada Maker. 


## **Maker Vaults**

Todos os ativos de garantia aceitos podem ser utilizados para gerar Dai no Protocolo Maker por meio de contratos inteligentes chamados Maker Vaults. O usuário pode acessar o Protocolo Maker e criar cofres utilizando diferentes interfaces (ou seja, portais de acesso à rede), inclusive [Oasis Borrow](https://oasis.app/borrow) e [várias outras desenvolvidas pela comunidade](https://makerdao.com/en/ecosystem). Não é difícil criar um cofre, mas a geração de Dai cria uma obrigação de pagamento dessa moeda, juntamente com uma 
<span class="annotated">Taxa de estabilidade<span class="annotation">A Taxa de estabilidade é um valor que deve ser pago por todo titular de um cofre quando a dívida é liquidada ou parcialmente quitada. Consiste em um rendimento percentual anual, calculado sobre a dívida existente do cofre. Essa taxa só pode ser paga em Dai.</span></span>
para que seja possível sacar a garantia alavancada e bloqueada no cofre. 

Cofres inerentemente não exigem custódia: os usuários interagem com o cofre e com o Protocolo Maker diretamente. Cada usuário tem controle total e autônomo sobre a garantia depositada, desde que o valor da garantia não atinja um nível inferior ao mínimo exigido (o Coeficiente de liquidação, discutido detalhadamente abaixo).


### Interação com o Maker Vault



*   **Etapa 1:​ criação do cofre e depósito da garantia**

    O usuário cria um cofre por meio do portal Oasis Borrow ou de uma interface desenvolvida pela comunidade, como Instadapp, Zerion ou MyEtherWallet. Para isso, é preciso adicionar um tipo e valor específico de garantia que será, então, usado para gerar Dai. Depois de adicionados os recursos, o cofre é considerado garantido. 

*   **Etapa​ ​2:​ geração de Dai​ a partir do cofre garantido**

    O titular do cofre inicia uma transação e, em seguida, faz a confirmação dessa transação na sua carteira de criptomoedas não hospedada a fim de gerar uma quantia específica de Dai. Em troca, sua garantia permanece bloqueada no Cofre.

*   **Etapa​ ​3:​ pagamento da dívida e da Taxa de estabilidade**

    Para recuperar a totalidade ou uma parte da garantia, o titular do Cofre precisa quitar parcial ou totalmente a dívida em Dai acrescida da Taxa de estabilidade que incide sobre essa dívida em Dai ao longo do tempo. A Taxa de estabilidade só pode ser paga em Dai.

*   **Etapa 4:​ ​saque da garantia**

    Com o Dai devolvido e a Taxa de estabilidade paga, o titular do Cofre pode sacar toda ou parte da garantia para sua carteira. Após a devolução completa do Dai e o saque de toda a garantia, o cofre permanece vazio até que o titular queira fazer outro depósito.

É importante destacar que cada ativo de garantia depositado requer seu próprio cofre. Dessa forma, alguns usuário vão ser titulares de vários cofres com diferente tipos e níveis de garantia.


### Liquidação de Maker Vaults de risco

Para garantir um nível permanente de garantias no Protocolo Maker a fim de cobrir o valor de todas as dívidas pendentes (a quantia em Dai pendente avaliada de acordo com o 
<span class="annotated">Preço de referência<span class="annotation">O Preço de referência para o Dai é 1 USD, indexado em 1:1 em relação ao dólar, no regime cambial intermediário.</span></span>),
todo Maker Vault considerado de alto risco (de acordo com os parâmetros estabelecidos pela Governança Maker) é liquidado por meio de leilões automatizados no Protocolo Maker. O Protocolo estabelece essa determinação após comparar o
<span class="annotated">Coeficiente de liquidação<span class="annotation">O Coeficiente de liquidação é o coeficiente de garantia sobre a dívida a partir do qual um Cofre fica sujeito à Liquidação.</span></span>
ao coeficiente de garantia sobre a dívida atual de um Cofre. Cada tipo de Cofre possui seu próprio Coeficiente de liquidação, controlado pelos titulares de MKR votantes e estabelecido com base no perfil de risco do ativo de garantia específico.


### Leilões do Protocolo Maker

Os [mecanismos de leilão](https://docs.makerdao.com/auctions/the-auctions-of-the-maker-protocol) do Protocolo Maker permitem que o sistema liquide Cofres mesmo quando não há informações disponíveis sobre o preço da garantia. No momento de liquidação, o Protocolo Maker vende a garantia que está no Cofre liquidado por meio de um mecanismo de leilão interno baseado no mercado. Trata-se de um 
<span class="annotated">Leilão de garantia<span class="annotation">Em um Leilão de garantia, o arrematante paga em Dai pela garantia de um Cofre liquidado. O Dai recebido é utilizado para cobrir a dívida vencida do Cofre, bem como a multa de liquidação.</span></span>. 

O Dai recebido com o Leilão da garantia é utilizado para cobrir as obrigações pendentes do Cofre, inclusive a taxa denominada 
<span class="annotated">Multa de liquidação<span class="annotation">A Multa de liquidação é uma taxa paga pelo titular no ato da liquidação do seu Cofre.</span></span>
estabelecida pelos titulares de MKR votantes para aquele tipo de garantia específica do Cofre.

Se houver lances de Dai suficientes para cobrir totalmente as obrigações do Cofre e a Multa de liquidação, o Leilão de garantia em questão converte-se em um
<span class="annotated">Leilão reverso de garantia<span class="annotation">Em um Leilão reverso, os Guardiões dão como lance partes cada vez menores da garantia que eles estão dispostos a aceitar por uma quantidade fixa de Dai. Esse processo é parte do Leilão de garantia e só será iniciado se houver interesse inicial suficiente na garantia para cobrir o valor de Dai pendente do Cofre. Se uma quantia suficiente de Dai for oferecida para cobrir essas obrigações, é acionado o Leilão reverso de garantia. A finalidade do Leilão reverso de garantia é ser um processo que dá ao titular do Cofre a melhor chance de recuperar a maior parte possível da garantia e, ao mesmo tempo, possibilita que todas as obrigações pendentes em Dai sejam cumpridas.</span></span>
na tentativa de vender a menor parte possível da garantia. O que restar da garantia é devolvido ao titular original do Cofre.

Se o Leilão de garantia não arrecadar Dai suficiente para cobrir as obrigações pendentes do Cofre, a diferença é convertida em dívida do Protocolo. Essa dívida é coberta pelo Dai contido na
<span class="annotated">Reserva Maker<span class="annotation">A Reserva Maker contém os recursos em Dai provenientes do Leilão de garantia (inclusive as Multas de liquidação), bem como das Taxas de estabilidade nos Cofres. Quando a quantia de Dai na Reserva Maker alcança um valor específico (determinado pela Governança Maker), o excedente é levado a um Leilão de excedente e é utilizado para a compra e remoção de MKR da oferta total. O valor excedente é o valor líquido das dívidas do sistema, como obrigações não liquidadas do Cofre em um Leilão de garantia e provisões da Taxa de poupança do Dai</span></span>.
Se não houver Dai suficiente na Reserva, o Protocolo aciona um
<span class="annotated">Leilão de dívida<span class="annotation">Leilões de dívida são utilizados para recapitalizar o sistema com leilões de MKR por um valor fixo de Dai.</span></span>.
Durante um Leilão de dívida, o MKR é emitido pelo sistema (o que aumenta o volume de MKR em circulação) e, em seguida, vendido a arrematantes por Dai.

Os recursos em Dai obtidos no Leilão de garantia são adicionados à Reserva Maker, cujo objetivo é evitar aumentos na oferta total de MKR provocados por Leilões futuros de garantia sem cobertura e pelas provisões da Taxa de poupança do Dai (discutida detalhadamente abaixo).

Se os recursos em Dai obtidos com os Leilões e pagamentos da Taxa de estabilidade excederem o limite da Reserva Maker (valor definido pela Governança Maker), eles são vendidos por meio de um 
<span class="annotated">Leilão de excedente<span class="annotation">Em um Leilão de excedente, o arrematante paga MKR por Dai excedente proveniente das Taxas de estabilidade. O MKR recebido é destruído, reduzindo assim o volume de MKR em circulação</span></span>.
Durante um Leilão de excedente, os participantes dão como lance parcelas cada vez menores de MKR para receberem um valor fixo em Dai. Após o encerramento do Leilão de excedente, o Protocolo Maker destrói de maneira autônoma o MKR recolhido, reduzindo assim a oferta total de MKR. 

[[observação]]
|<span class="note-heading">Exemplo (processo de Leilão de garantia):</span>
|*Um Cofre com grande quantia fica subgarantido em virtude das condições de mercado. Em seguida, um 
|<span class="annotated">Guardião de leilões<span class="annotation">O Guardião de leilões é uma pessoa ou um bot automatizado que recebe incentivos do Protocolo Maker para monitorar o sistema e acionar a liquidação quando o Coeficiente de liquidação do Cofre é atingido.</span></span>
|detecta a oportunidade criada pelo Cofre subgarantido e inicia a liquidação do mesmo com o Leilão de garantia de, por exemplo, 50 ETH.*
|
|*Cada [Guardião de leilões](https://blog.makerdao.com/introduction-to-auctions-and-keepers-in-mcd/) tem um 
|<span class="annotated">modelo de lances<span class="annotation">Um modelo de lances é a estratégia que define quando, com que frequência e a que preço fazer lances.</span></span>
|para viabilizar leilões bem-sucedidos. Um modelo de lances inclui o preço da garantia (ETH, nesse exemplo) que deve disparar os lances. O Guardião de leilões utiliza o preço do token em seu modelo de lances como base para os lances na primeira fase do Leilão de garantia, quando são feitos lances crescentes de Dai por um valor fixo da garantia. Esse valor representa o preço do total de Dai que se deseja obter com o leilão da garantia.* 
|
|*Agora, digamos que o Guardião de leilões dê um lance de 5.000 Dai pelos 50 ETH de forma a cobrir o valor de ETH. O lance de Dai é transferido do 
|<span class="annotated">Mecanismo de Cofre<span class="annotation">O Mecanismo de Cofre é o contrato inteligente de VAT. Para obter mais informações, acesse https://docs.makerdao.com/other-documentation/system-glossary#vat-vault-engine.</span></span>
|para o contrato do Leilão de garantia. Com Dai suficiente no contrato do Leilão de garantia para cobrir a dívida do sistema e a Multa de liquidação, a primeira fase do Leilão de garantia está encerrada.* 
|
|*Para atingir o preço definido em seu modelo de lances, o Guardião de leilões envia um lance na segunda fase do Leilão de garantia. Nessa fase, o objetivo é devolver ao titular do Cofre a maior parte da garantia que o mercado permitir. Os lances feitos pelos Guardiões de leilões são de valores fixos de Dai e valores decrescentes de ETH. Por exemplo, o modelo de lances do Guardião neste exemplo busca atingir um preço de lance de 125 Dai por ETH. Assim, ele oferece 5.000 Dai por 40 ETH. O valor adicional em Dai para esse lance é transferido do Mecanismo de Cofre para o contrato do Leilão de garantia. Limite de duração do lance atingido e lance expirado, o Guardião de leilões é considerado o vencedor e finaliza o Leilão ao arrematar a garantia obtida.*


## **Principais agentes externos**

Além da sua infraestrutura de contratos inteligentes, o Protocolo Maker envolve grupos de agentes externos para manter as operações: Guardiões, Oráculos e Liquidadores globais (Oráculos de emergência) e membros da comunidade Maker. Guardiões aproveitam os incentivos econômicos oferecidos pelo Protocolo. Oráculos e Liquidadores globais são agentes externos que recebem permissões especiais no sistema concedidas pelos proprietários de MKR com direito a voto. Já membros da comunidade Maker são pessoas e organizações que prestam serviços.


### **Guardiões**

O Guardião é um agente independente (geralmente automatizado) que recebe incentivos na forma de oportunidades de arbitragem para oferecer liquidez em vários aspectos de um sistema descentralizado. No Protocolo Maker, os [Guardiões integram o mercado que ajuda o Dai a manter seu Preço de referência](https://docs.makerdao.com/keepers/market-maker-keepers) (1 USD): eles vendem Dai quando o preço de mercado fica acima do Preço de referência e compram quando esse preço fica abaixo do Preço de referência. Eles participam de Leilões de excedente, dívida e garantia durante a Liquidação dos Maker Vaults.


### **Oráculos de preço**

Para saber quando acionar as Liquidações, o Protocolo Maker requer informações em tempo real sobre o preço de mercado dos ativos de garantia nos Maker Vaults. 

O Protocolo calcula os preços internos da garantia por uma [infraestrutura de Oráculo descentralizada](https://blog.makerdao.com/introducing-oracles-v2-and-defi-feeds/) que consiste em um amplo conjunto de nós individuais chamados de Feeds de oráculo. Os titulares de MKR votantes escolhem um grupo de Feeds confiáveis para transmitir informações de preço ao Protocolo Maker por meio de transações em Ethereum. Eles também controlam o número de Feeds que integram o conjunto.

Para proteger o sistema de tentativas de ataque que queiram assumir o controle da maioria dos Oráculos, o Protocolo Maker recebe informações de preço do [Módulo de segurança de oráculos](https://docs.makerdao.com/smart-contract-modules/oracle-module/oracle-security-module-osm-detailed-documentation) (OSM, na sigla em inglês), e não diretamente dos Oráculos. A camada de defesa entre os Oráculos e o Protocolo, o OSM informa o preço com atraso de uma hora, permitindo que Oráculos de emergência ou uma votação da Governança Maker congelem o Oráculo comprometido. As decisões relacionadas aos Oráculos de emergência e à duração do atraso são tomadas por titulares de MKR.   


### **Oráculos de emergência**

Os Oráculos de emergência são selecionados por titulares de MKR votantes e agem com a última linha de defesa contra um ataque ao processo de governança ou a outros Oráculos. Eles podem congelar Oráculos específicos (por exemplo, Oráculos BAT ou ETH) para reduzir o risco de que um grande número de clientes saque ativos do Protocolo Maker durante um curto período. Para isso, eles têm autoridade para acionar unilateralmente uma 
<span class="annotated">Desativação de emergência<span class="annotation">A Desativação de emergência tem duas funções principais. É usada em emergências como último recurso para proteger o Protocolo Maker contra ataques à infraestrutura e também para promover a atualização do sistema do Protocolo Maker. O processo é completamente descentralizado e controlado pela Governança Maker</span></span>.  


### **Equipes DAO**

As Equipes DAO são formadas por indivíduos e prestadores de serviços que podem ser contratados pela Governança Maker para prestar serviços específicos para a MakerDAO. Os membros das Equipes DAO são agentes do mercado autônomos e não são funcionários da Fundação Maker.

A flexibilidade da Governança Maker permite que a comunidade Maker adapte a estrutura das Equipes DAO para a prestação dos serviços necessários ao ecossistema com base em desempenho real e desafios emergentes.

Como exemplos das funções dos membros das Equipes DAO, é possível citar o Facilitador de governança, responsável por dar suporte à infraestrutura e aos processos de comunicação da governança, e os membros da Equipe de risco, que dão suporte à Governança Maker no que diz respeito a pesquisas e propostas preliminares de risco financeiro para a integração de uma nova garantia e para o controle das garantias já existentes. 

Embora a Fundação Maker tenha financiado a Governança Maker até o momento, a previsão é de que, em breve, a Organização autônoma descentralizada (DAO, na sigla em inglês) assumirá o controle total, conduzirá as votações de MKR e assumirá essas diversas funções da Equipe DAO.


## **A Taxa de poupança do Dai**

A [Taxa de poupança do Dai (DSR) permite que todo titular de Dai gere poupança](https://blog.makerdao.com/why-the-dai-savings-rate-is-a-game-changer-for-the-defi-ecosystem-and-beyond/) de forma nativa e automática ao bloquear seu Dai em um contrato DSR no Protocolo Maker. Ela pode ser acessada por meio do portal [Oasis Save](https://oasis.app/save) ou pelos [vários gateways](https://makerdao.com/en/ecosystem) de acesso ao Protocolo Maker. O usuário não precisa depositar um valor mínimo para ganhar DSR. Além disso, ele pode sacar todo ou uma parte de seu Dai do contrato DSR quando quiser.    

A DSR é um parâmetro global do sistema que determina o valor que o titular de Dai deve auferir sobre sua poupança ao longo do tempo. Quando o preço de mercado do Dai diverge do Preço de referência devido a mudanças nas dinâmicas do mercado, os titulares de MKR podem eliminar a instabilidade de preço ao votarem para alterar a DSR de acordo com o contexto: 

*   Se o preço de mercado do Dai estiver acima de 1 USD, os titulares de MKR podem optar por reduzir gradualmente a DSR, o que diminui a demanda e deve diminuir também o preço de mercado do Dai na direção do Preço de referência de 1 USD.
*   Se o preço de mercado do Dai estiver abaixo de 1 USD, os titulares de MKR podem optar por aumentar gradualmente a DSR, o que amplia a demanda e deve elevar o preço de mercado do Dai na direção do Preço de referência de 1 USD.

No começo, o ajuste da DSR depende de um processo semanal, no qual os titulares de MKR primeiro avaliam e discutem dados públicos de mercado e dados proprietários fornecidos pelos participantes do mercado e, em seguida, votam se é ou não necessário fazer um ajuste. O plano de longo prazo inclui a implementação do Módulo de ajuste da DSR, um 
<span class="annotated">Módulo de acesso instantâneo<span class="annotation">Um Módulo de acesso instantâneo contém componentes para a criação de mudanças limitadas e diretas ao Protocolo Maker sem consenso no DS-Chief.</span></span>
que controla diretamente tanto a DSR quanto a 
<span class="annotated">Taxa base<span class="annotation">A Taxa base faz parte da Taxa de estabilidade que é aplicada a todos os tipos de ativos (ou seja, a Taxa de estabilidade total de cada tipo de ativo inclui a Taxa base e a Taxa de garantia).</span></span> 
Esse módulo facilita o ajuste à DSR (dentro dos rígidos limites de frequência e grandeza definidos pelos titulares de MKR) por um titular de MKR em nome do grupo de titulares de MKR. O objetivo desse plano é possibilitar respostas ágeis a condições de mercados em constante mutação e evitar o uso excessivo dos processos padrão de governança: as Votações executivas e as Votações de governança.


## **Governança do Protocolo Maker**


### **Uso do token MKR na Governança Maker**

O token de governança do Protocolo Maker, chamado MKR, permite que seus titulares _votem_ nas mudanças ao Protocolo Maker. É importante destacar que qualquer pessoa, e não apenas titulares de MKR, pode _enviar_ propostas de votação MKR. 

É provável que, no futuro, as alterações aprovadas por voto às variáveis de governança do Protocolo não comecem a vigorar imediatamente. Muito pelo contrário: elas poderão demorar até 24 horas se os votantes decidirem ativar o Módulo de segurança da governança (GSM, na sigla em inglês). O atraso dá aos titulares de MKR a chance de acionar uma Desativação, a fim de proteger o sistema contra uma proposta de governança maliciosa, se necessário. Por exemplo, uma proposta que altere os parâmetros de garantia para que contrariem as políticas monetárias estabelecidas ou que permita a desativação de mecanismos de segurança.  

**Consultas de proposta e Votações executivas.**

Na prática, o processo de Governança Maker inclui Consultas de proposta e Votações executivas. As Consultas de proposta são realizadas para estabelecer um consenso aproximado que reflita a visão da comunidade antes da realização de Votações executivas. Assim, procura-se garantir que as decisões de governança sejam cuidadosamente avaliadas e alcancem o consenso antes do início do processo de votação. As Votações executivas são conduzidas para aprovar ou não as alterações ao estado do sistema. Um exemplo dessas votações seria a votação para ratificar os Parâmetros de risco de um tipo de garantia que acabou de ser aceito. 

No nível técnico, contratos inteligentes gerenciam cada tipo de votação. Um Contrato de proposta é um contrato inteligente que tem programada pelo menos uma ação de governança válida. Ele só pode ser executado uma vez. Quando executado, ele aplica imediatamente as alterações às variáveis de governança interna do Protocolo Maker e, depois, não pode mais ser utilizado.

Qualquer 
<span class="annotated">Endereço Ethereum<span class="annotation">Uma Conta de contrato Ethereum é controlada por seu código de contrato. Ela não pode dar início a novas transações por si só. Apenas ao receber uma mensagem de uma conta de terceiros ou de outra Conta de contrato é que ela pode executar seu próprio código, permitindo a leitura, gravação e envio de mensagens ou a criação de contratos inteligentes.</span></span>
pode implementar Contratos de proposta válidos. Os titulares de MKR votantes podem, então, votar pela aprovação da proposta que desejam escolher como a Proposta ativa. O Endereço Ethereum com o maior número de votos de aprovação é escolhido como a Proposta ativa. A Proposta ativa é autorizada a obter acesso administrativo às variáveis de governança internas do Protocolo Maker e alterá-las. 

**O papel do token MKR na recapitalização**

Além da sua função na Governança Maker, o token MKR desempenha outro papel: recurso de recapitalização do Protocolo Maker. Se a dívida do sistema supera o excedente, a oferta de token MKR pode aumentar por meio de um Leilão de dívida (veja acima) a fim de recapitalizar o sistema. Essa possibilidade leva os titulares de MKR a alinhar e governar com responsabilidade o ecossistema Maker para evitar riscos excessivos.

**Responsabilidades do titular de MKR**

O titular de MKR pode votar para executar as seguintes ações:



*   Adicionar um novo tipo de garantia com um conjunto exclusivo de Parâmetros de risco. 
*   Alterar ou incluir novos Parâmetros de risco a um ou mais tipos de ativo de garantia já existentes.
*   Alterar a Taxa de poupança do Dai.
*   Escolher o conjunto de Feeds de oráculo.
*   Escolher o conjunto de Oráculos de emergência. 
*   Acionar a Desativação de emergência.
*   Atualizar o sistema.

Os titulares de MKR também podem alocar recursos da Reserva Maker para o pagamento de diversos serviços e requisitos de infraestrutura, inclusive para a infraestrutura de Oráculo e pesquisas de gerenciamento de risco de garantia. Os recursos na Reserva Maker são as receitas de Taxas de estabilidade, Taxas de liquidação e outras fontes de renda.

O mecanismo de governança do Protocolo Maker foi desenvolvido para ser o mais flexível possível e passível de atualização. Se o sistema evoluir com base nas orientações da comunidade, formas mais avançadas de Contratos de proposta poderão teoricamente ser utilizadas, inclusive Contratos de proposta agrupados. Por exemplo, um Contrato de proposta pode conter tanto um ajuste a uma Taxa de estabilidade quanto um ajuste à DSR. Entretanto, essas revisões ficarão a critério dos titulares de MKR.


### **Parâmetros de risco controlados pela Governança Maker**

Cada tipo de Maker Vault (por exemplo, Cofre de ETH ou de BAT) tem o próprio conjunto de Parâmetros de risco que regem seu uso. Esses parâmetros são determinados com base no perfil de risco da garantia e controlados diretamente pelos titulares de MKR por meio de votação.

**Os principais Parâmetros de risco para Maker Vaults são:**



*   **Teto de dívida**: trata-se do montante máximo de dívida que pode ser criado por um único tipo de garantia. A Governança Maker atribui a cada tipo de garantia um Teto de dívida, que é usado para garantir que haja diversificação suficiente na carteira de garantias do Protocolo Maker. Quando a garantia atinge o Teto de dívida específico, torna-se impossível aumentar a dívida, a não ser que usuários já existentes quitem a dívida total ou parcial de seus Cofres.
*   **Taxa de estabilidade**: consiste em um rendimento percentual anual, calculado sobre o valor de Dai gerado face à garantia do Cofre. A Taxa, que só pode ser paga em Dai, é então enviada para a Reserva Maker.
*   **Coeficiente de liquidação**: um Coeficiente de liquidação baixo significa que a Governança Maker espera uma baixa volatilidade dos preços da garantia, enquanto um Coeficiente elevado significa que ela espera alta volatilidade.
*   **Multa de liquidação**:​ quando da liquidação de um Cofre, trata-se de uma taxa adicionada ao total não liquidado gerado em Dai. A Multa de liquidação é usada para incentivar os titulares de Cofres a manterem níveis adequados de garantia.
*   **Duração do Leilão de garantia**: a duração máxima dos Leilões de garantia é específica de cada Maker Vault. Já as durações dos Leilões de dívida e de excedente são parâmetros globais do sistema.
*   **Duração dos lances de leilão:** período até a expiração de um lance específico, encerrando o leilão.
*   <span class="annotated">Mínimo por etapa do leilão****<span class="annotation">O valor mínimo que um participante pode oferecer acima do lance anterior durante um leilão.</span></span> Esse Parâmetro de risco existe para incentivar os primeiros lances nos leilões e evitar abusos, como um lance que oferece um valor irrisório a mais do que o lance anterior.


### **Responsabilidades da Governança com a mitigação de riscos**

Para que a operação do Protocolo Maker seja bem-sucedida, é preciso que a Governança Maker tome as medidas necessárias para reduzir o risco. Abaixo, seguem alguns desses riscos e seus planos de mitigação.

#### **Ataque à infraestrutura de contratos inteligentes por um agente malicioso.**

Um dos maiores riscos ao Protocolo Maker é o agente malicioso. Por exemplo, um programador que descobriu uma vulnerabilidade nos contratos inteligentes implementados e utiliza essa informação para invadir o Protocolo e defraudá-lo.

No pior dos casos, todos os ativos digitais descentralizados mantidos como garantia no Protocolo são roubados, sem possibilidade de recuperação.

**Mitigação:** A maior prioridade da Fundação Maker é a [segurança do Protocolo Maker](https://blog.makerdao.com/mcd-security-roadmap-update-october-2019/), e a defesa mais robusta do Protocolo é a 
<span class="annotated">Verificação formal<span class="annotation">Por Verificação formal, entende-se a criação de especificações matemáticas acerca do comportamento esperado do sistema, juntamente com provas matemáticas que garantam que a base de código de fato implementa um comportamento idêntico ao esperado, sem que haja nenhum efeito colateral não intencional, já que não há evidência matemática para isso</span></span>. 
A base de código do Dai foi a primeira na esfera das aplicações descentralizadas a ser [formalmente verificada](https://forum.makerdao.com/t/publication-of-the-runtime-verification-audit/976). 

Além da verificação formal do sistema, auditorias de segurança contratadas conduzidas pelas melhores empresas de segurança no setor de blockchain, auditorias externas (independentes) e recompensas para identificação de bugs são parte do [esquema de segurança da Fundação](https://blog.makerdao.com/mcd-security-roadmap-update-october-2019/). Para consultar o relatório de verificação formal e diversas auditorias do Protocolo Maker, acesse o [repositório Github de Segurança do Dai com garantias múltiplas](https://github.com/makerdao/mcd-security) do Maker.

Essas medidas de segurança viabilizam um sistema de defesa potente. Contudo, não são infalíveis. Mesmo com a Verificação formal, a modelagem matemática dos comportamentos esperados pode estar incorreta ou as suposições que informam o comportamento esperado podem, elas mesmas, estar incorretas. 

#### **Evento do tipo Cisne negro**

Um evento Cisne negro consiste em um raro ataque crítico surpresa ao sistema. No caso do Protocolo Maker, exemplos de um evento desse tipo incluem:

*   Um ataque aos tipos de garantia do Dai.  
*   Uma redução alta e inesperada relativa a um ou mais tipos de garantia. 
*   Um ataque de oráculo altamente coordenado.  
*   Uma proposta maliciosa à Governança Maker

É importante destacar que essa lista de cisnes negros em potencial não é exaustiva e não tem como objetivo citar toda a multiplicidade de possibilidades existentes.

**Mitigação:** Embora nenhuma solução seja completamente livre de falhas, o design cuidadoso do Protocolo Maker (com seus Coeficiente de liquidação, Tetos de dívida, Módulo de segurança da governança, Módulo de segurança de oráculos, Desativação de emergência etc.) ajuda a evitar ou mitigar as possíveis consequências sérias de um ataque.

#### **Erros inesperados de preço e irracionalidade do mercado**

É possível que ocorram problemas no Feed de preço dos Oráculos ou dinâmicas irracionais de mercado, provocando variações prolongadas no valor do Dai. Se houver perda de confiança no sistema, os ajustes de taxa ou mesmo a diluição de MKR poderão atingir níveis extremos e, ainda assim, não resultar em liquidez e estabilidade suficientes para o mercado.

**Mitigação: ** a Governança Maker procura incentivar um pool de capital grande o suficiente para funcionar como Guardiões do mercado. O objetivo é maximizar a racionalidade e a eficiência e permitir que a oferta de Dai cresça a um ritmo constante, sem grandes choques de mercado. Como último recurso, a Desativação de emergência pode ser acionada para liberar as garantias aos titulares de Dai, sendo que suas reivindicações de Dai são avaliadas pelo Preço de referência.

#### **Migração de usuários para soluções mais simples**

O Protocolo Maker é um sistema descentralizado complexo. Como resultado, há o risco de que usuários inexperientes de criptomoedas migrem do Protocolo para sistemas que sejam mais fáceis de usar e entender. 

**Mitigação: ** embora a geração e o uso do Dai sejam simples para a maioria dos entusiastas de criptomoedas e para os Guardiões que utilizam a moeda para negociação com margem, pessoas com menos experiência podem considerar o Protocolo difícil de entender e utilizar. Embora o Dai tenha sido desenvolvido para que o usuário não precisa compreender a mecânica subjacente do Protocolo Maker para aproveitar seus benefícios, [a documentação e os inúmeros recursos](https://docs.makerdao.com/) disponibilizados pela comunidade Maker e pela Fundação Maker ajudam a garantir que a integração ao sistema ocorra da forma mais simples possível.

#### **Dissolução da Fundação Maker**

Juntamente com agentes independentes, a Fundação Maker tem a função de manter o Protocolo Maker e ampliar seu uso globalmente, além de viabilizar a Governança. No entanto, a Fundação Maker planeja sua dissolução quando o MakerDAO puder gerenciar a Governança por si só. Se o MakerDAO não conseguir dar conta de suas funções quando da dissolução da Fundação Maker, a integridade futura do Protocolo Maker pode ficar em risco.

**Mitigação:** os titulares de MKR recebem incentivos para se prepararem para a dissolução da Fundação, programada para ocorrer depois que ela concluir a “descentralização gradual” do projeto. Além disso, o gerenciamento bem-sucedido do sistema deve resultar na geração de recursos suficientes para que a Governança possa dar continuidade à manutenção e ao aprimoramento do Protocolo Maker.

#### **Problemas gerais com tecnologia experimental**

Os usuários do Protocolo Maker (inclusive, entre outros, os titulares de Dai e MKR) compreendem e aceitam que o software, a tecnologia e as teorias e conceitos técnicos aplicáveis ao Protocolo Maker ainda não foram comprovados, e não há garantia de que a tecnologia permanecerá sem erros ou interrupções. Há o risco inerente de que a tecnologia contenha pontos fracos, vulnerabilidades ou bugs, gerando, entre outras coisas, a falha total do Protocolo Maker e/ou de suas partes constitutivas. 

**Mitigação:** Consulte “Ataque à infraestrutura de contratos inteligentes por um agente malicioso” acima. A seção Mitigação explica a auditoria técnica estabelecida para garantir que o Protocolo Maker funcione como pretendido.


## **Mecanismos de estabilidade de preços**


### **O Preço de referência do Dai**

O Preço de referência do Dai é usado para determinar o valor dos ativos de garantia recebidos por titulares de Dai no caso de uma Desativação de emergência. O Preço de referência para o Dai é 1 USD, indexado em 1:1 em relação ao dólar, no regime cambial intermediário.  


### **Desativação de emergência.**

A Desativação de emergência (ou simplesmente Desativação) tem duas funções principais. Em primeiro lugar, ela é usada em emergências como último recurso para proteger o Protocolo Maker contra ataques à infraestrutura e para aplicar diretamente o Preço de referência do Dai. Entre as emergências, estão atividades maliciosas da Governança, invasões, falhas de segurança e irracionalidade de mercado de longo prazo. Em segundo lugar, ela deve promover a atualização do sistema do Protocolo Maker. O processo de Desativação é controlado exclusivamente pela Governança Maker.

Se um número suficiente de titulares de MKR votantes julgar necessário, eles também podem acionar uma Desativação de emergência depositando MKR no Módulo de desativação de emergência (ESM). Esse procedimento evita que o Módulo de segurança da governança (se ativo) atrase as propostas de Desativação antes que sejam executadas. Assim que alcançado o quórum, a Desativação de emergência passa a vigorar imediatamente.  

**A Desativação de emergência apresenta três fases:**



1. **O Protocolo Maker é desativado, e os titulares dos Cofres sacam seus ativos.**

    Quando iniciada, a Desativação impede a criação de novos Cofres e a manipulação de Cofres já existentes, além de congelar os Feeds de preço. O congelamento dos Feeds garante que todos os usuários consigam sacar o valor líquido dos ativos a que têm direito. Isso permite que os titulares de Maker Vaults saquem imediatamente as garantias de seus Cofres que não estejam sendo usadas como lastro de dívida.

2. **Processamento de leilões após a Desativação de emergência**

    Após o acionamento da Desativação, os Leilões de garantia têm início e devem ser concluídos dentro de um prazo específico. Esse período é determinado pela Governança Maker e precisa durar um pouco mais do que o Leilão de garantia mais longo. Essa diretiva garante que nenhum leilão fique pendente após a conclusão do período de processamento de leilões.

3. **​Titulares de Dai reivindicam a garantia restante**

    Ao final do prazo de processamento de leilões, os titulares de Dai utilizam a criptomoeda para reivindicar diretamente garantias a uma taxa fixa que corresponde ao valor calculado de seus ativos com base no Preço de referência do Dai. Por exemplo, se o preço de ETH/USD for 200 e um usuário possuir 1000 Dai com Preço de referência de 1 USD no acionamento da Desativação de emergência, ele poderá reivindicar exatamente 5 ETH do Protocolo Maker após o período de processamento de leilões. Não há prazo para a reivindicação final. Os titulares de Dai terão direito a uma reivindicação proporcional a cada tipo de garantia existente na carteira de garantias. É importante destacar que titulares de Dai correm o risco de sofrer cortes, o que significa que não receberão o valor total de suas posses em Dai com Preço de referência de 1 USD por Dai. Isso se deve tanto aos riscos relacionados à queda de valor das garantias quanto ao direito dos titulares de Cofres de recuperarem o excedente de suas garantias antes que os titulares de Dai possam reivindicar o restante. Para obter informações mais detalhadas sobre a Desativação de emergência, incluindo as prioridades de reivindicação que podem ocorrer como resultado, consulte a [documentação publicada na comunidade](https://community-development.makerdao.com/makerdao-mcd-faqs/faqs/emergency-shutdown). 


# **O futuro do Protocolo Maker: aumento da adoção e descentralização total**

### **Mercado disponível**

Uma criptomoeda com preço estável funciona como um importante meio de troca para diversas aplicações descentralizadas. Assim, o mercado potencial para o Dai é, pelo menos, tão grande quanto todo o setor descentralizado de blockchain. No entanto, as possibilidades descortinadas pelo Dai vão além, abarcando outros setores. 

Abaixo, segue uma lista não exaustiva de mercados atuais para a stablecoin Dai:

*   **Capital de giro, operações de hedge e margem de garantia**. Os Maker Vaults possibilitam que o usuário realize negociações sem necessidade de permissão e, então, use o Dai gerado pela garantia do Cofre para gerar capital de giro. Já houve várias situações em que o titular de Cofre usou seu Dai para comprar mais ETH (o mesmo ativo da sua garantia), criando, assim, uma posição alavancada, mas totalmente garantida.
*   **Recibos de comerciantes, remessas e transações internacionais**. A mitigação da volatilidade cambial e a eliminação dos intermediários significam que os custos de transações de comércio internacional são significativamente reduzidos com o Dai.
*   **Instituições de caridade e ONGs** que usam a tecnologia de registro distribuído transparente. 
*   **Jogos**. Para desenvolvedores de jogos que usam a tecnologia blockchain, o Dai é a moeda preferencial. Com o Dai, esses desenvolvedores não integram apenas uma moeda, mas uma economia inteira. A modularidade do Dai permite que os jogos criem novos esquemas de comportamento de jogador com base em finanças descentralizadas.
*   **Mercados preditivos**. Ao fazer uma previsão não relacionada, é óbvio que não se deseja aumentar o próprio risco fazendo uma aposta com uma criptomoeda volátil. As apostas de longo prazo tornam-se especialmente inviáveis se o apostador também tiver que apostar no preço futuro do ativo volátil usado para fazer a aposta. Sendo assim, a stablecoin Dai é a escolha natural para uso em mercados preditivos.


### **Expansão de ativos**

Se os titulares de MKR aprovarem novos ativos como garantia, esses ativos estarão sujeitos aos mesmos requisitos de risco, parâmetros e medidas de segurança que o Dai (por exemplo, Coeficientes de liquidação, Taxas de estabilidade, Taxas de poupança, Tetos de dívida, etc.).


### **Oráculos em evolução**

O MakerDAO foi o primeiro projeto a executar Oráculos confiáveis na blockchain Ethereum. Como resultado, muitas aplicações descentralizadas utilizam os Oráculos MakerDAO para garantir a segurança de seus sistemas e fornecer dados atualizados de preço com rigor. Tal confiança no MakerDAO e no Protocolo Maker significa que a Governança Maker pode expandir o serviço central da infraestrutura de Oráculos para melhor atender às necessidades das aplicações descentralizadas. 


# **Conclusão**

O Protocolo Maker permite que o usuário gere Dai, uma reserva estável de valor que existe exclusivamente na blockchain. O Dai é uma stablecoin descentralizada que não é emitida ou administrada por nenhum agente centralizador ou intermediário ou contraparte de confiança. É independente e internacional, disponível para qualquer um, em qualquer lugar. 

Todo Dai é garantido por um excedente depositado em contratos inteligentes Ethereum exibidos publicamente e auditados. Qualquer pessoa com conexão à Internet pode monitorar a integridade do sistema quando quiser acessando [daistats.com](https://daistats.com/).  

Com centenas de parcerias e uma das mais respeitadas comunidades de desenvolvedores no mundo das criptomoedas, o MakerDAO tornou-se o motor do movimento de finanças descentralizadas (DeFi). A Maker está ampliando as possibilidades de blockchain para fazer cumprir já a promessa de empoderamento econômico. 

Para obter mais informações, acesse o [site do MakerDAO](https://makerdao.com/en/).  


# **ANEXOS**

## **Exemplos e vantagens de casos de uso do Dai**

O Protocolo Maker pode ser usado por qualquer pessoa, sem nenhuma restrição nem exigência de dados pessoais. Abaixo, seguem alguns exemplos de como o Dai é usado em todo o mundo:


### **Dai oferece independência financeira para todos**

De acordo com o Global Findex Database 2017 do Banco Mundial, cerca de 1,7 bilhões de adultos no mundo inteiro são desbancarizados.[^5] Apenas nos EUA, de acordo com uma pesquisa de 2017 feita pela FDIC, cerca de 32 milhões de famílias norte-americanas são parcialmente bancarizadas ou desbancarizadas,[^6] o que significa que não dispõem de conta bancária ou utilizam regularmente alternativas ao sistema bancário tradicional (por exemplo, empréstimos de curto prazo ou em casas de penhor) para gerenciar suas finanças. O Dai pode empoderar cada uma dessas pessoas: basta que elas tenham acesso à Internet.

Como a primeira stablecoin independente, o Dai possibilita que qualquer pessoa alcance a independência financeira, não importa onde esteja ou suas circunstâncias. Por exemplo, na América Latina, o Dai possibilitou que indivíduos e famílias se protegessem conta a desvalorização do peso argentino[^7] e do bolívar venezuelano. Nas ilhas de Vanuatu, no Sul do Pacífico, onde os residentes pagam taxas de transferência monetária muito elevadas, a Oxfam International, ONG sediada no Reino Unido, juntou-se à startup australiana Sempo e à startup baseada em Ethereum ConsenSys, para criar um programa-piloto de assistência monetária. Duzentos residentes da ilha de Efate receberam 50 Dai que podiam ser usados com uma rede local de comerciantes.[^8] 


### **Geração de dinheiro autossoberana**

O Oasis Borrow permite que todos os usuários do Protocolo Maker gerem Dai ao bloquear garantias em Maker Vaults. Vale destacar que os usuários não precisam acessar intermediários externos para gerar Dai. Os Cofres oferecem a pessoas e empresas a chance de gerar liquidez com seus ativos de forma simples, rápida e relativamente barata.  


### **Poupança gerada automaticamente**

Titulares de Dai em qualquer lugar do mundo podem impulsionar sua inclusão financeira ao aproveitar a Taxa de poupança do Dai. Como discutido anteriormente, essa Taxa se baseia no valor do Dai, permitindo que o usuário lucre com o Dai que já possui e proteja suas economias da inflação. 

Por exemplo, se o Beto tem 100.000 Dai bloqueados em um contrato DSR, e o DSR definido pela Governança Maker é de 6% ao ano, ele vai gerar uma poupança de 6.000 Dai ao longo de 12 meses. Além disso, como as casas de câmbio e os projetos de blockchain podem integrar a DSR em suas próprias plataformas, ela cria novas oportunidades para que negociadores de criptomoedas, empreendedores e empresas consolidadas aumentem suas economias e capital operacional em Dai. Em razão desse mecanismo de atração, os formadores de mercado podem, por exemplo, escolher manter seu inventário inativo em Dai e bloqueá-lo na DSR. 


### **Remessas rápidas de baixo custo**

Sejam para a compra de bens ou serviços ou para o envio de dinheiro a familiares ou amigos, as remessas internacionais podem significar taxas elevadas de transferência e de serviço, longos prazos de entrega e problemas frustrantes de câmbio devido à inflação. A stablecoin Dai é usada em todo mundo como meio de troca pois as pessoas confiam em seu valor e eficiência.

Os usuários de remessas se beneficiam do Dai das seguintes maneiras:



*   **Transferências nacionais e internacionais de baixo custo.** O Dai proporciona economia imediata de custos, com as baixas taxas de 
<span class="annotated">GAS<span class="annotation">O GAS é uma unidade de medida que estabelece a taxa a ser paga por um usuário para a realização de uma transação na blockchain Ethereum. Todas as transações exigem certo valor do GAS.</span></span>
substituem as altas taxas cobradas por bancos e serviços de transferência. O baixo custo permite transações mais frequentes.
*   **Serviço ininterrupto.**  O Dai não depende do horário de funcionamento de bancos para realizar operações. O Protocolo Maker pode ser acessado sempre que for preciso.
*   **On-ramps e off-ramps convenientes.** O usuário pode aproveitar as diversas on-ramps e off-ramps que convertem moedas fiduciárias em Dai. Essas opções permitem que os usuários transitem entre as esferas da moeda fiduciária e da criptomoeda e consigam trocar suas posses em Dai pela moeda local com toda facilidade.
*   **Maior segurança e confiabilidade.** A blockchain oferece confiabilidade e segurança de alto nível.


### **Estabilidade em mercados voláteis**

Como destacado anteriormente, o Dai é tanto uma reserva de valor prontamente disponível quanto um poderoso meio de troca. Sendo assim, ele ajuda a proteger os negociantes contra a volatilidade. Por exemplo, o Dai oferece ao negociante uma forma simples de alternar entre posições sem dificuldade e permanecer ativo no mercado sem precisar sair das posições e repetir o ciclo de on-ramp/off-ramp.


### **Dai como fomentador do ecossistema e motor do DeFi**

Cada vez mais usuários estão tomando conhecimento do valor do Dai como stablecoin. Com isso, mais desenvolvedores estão integrando o Dai em seus dapps na blockchain Ethereum. Sendo assim, o Dai está ajudando a criar um ecossistema mais robusto. Em poucas palavras, o Dai permite que desenvolvedores de dapps ofereçam um método estável de troca a usuários que preferem não comprar ou vender bens e serviços usando ativos especulativos.  

Além disso, como o Dai pode ser usado para pagar por GAS no ecossistema Ethereum, ao criar dapps DeFi que aceitam Dai no lugar de ETH, os desenvolvedores proporcionam uma experiência de integração fácil e uma experiência melhor de maneira geral para os usuários. 


## **Glossários**

 



*   [Glossário de termos do MakerDAO](https://community-development.makerdao.com/makerdao-mcd-faqs/faqs/glossary)
*   [Glossário do Protocolo Maker](https://docs.makerdao.com/other-documentation/system-glossary) (termos, variáveis, funções e muito mais)


## **Recursos da comunidade e do sistema**



*   [MakerDAO no GitHub](https://github.com/makerdao/)​
*   [Documentações do MakerDAO](http://docs.makerdao.com/) 
*   [MakerDAO.com](https://makerdao.com/en/)
*   [Blog do MakerDAO](https://blog.makerdao.com/)
*   [Fórum do MakerDAO](https://forum.makerdao.com/)
*   [Chat do MakerDAO](https://chat.makerdao.com/)
*   [MakerDAO no Reddit](https://reddit.com/r/makerdao/)
*   [MakerDAO no Twitter](https://twitter.com/MakerDAO)

<!-- Footnotes themselves at the bottom. -->
## Observações

[^1]:
     é importante destacar que Organizações autônomas descentralizadas (DAOs) são definidas pela comunidade Ethereum como, em sua maioria, comunidades de cunho técnico e social centradas em uma missão ou projeto específico, não exigindo, portanto, a adoção de formas societárias tradicionais. 

[^2]:
     [https://ethereum.org/](https://ethereum.org/)

[^3]:
     [https://www.jpmorgan.com/global/news/digital-coin-payments](https://www.jpmorgan.com/global/news/digital-coin-payments)

[^4]:
     [https://libra.org/en-US/wp-content/uploads/sites/23/2019/06/LibraWhitePaper_en_US.pdf](https://libra.org/en-US/wp-content/uploads/sites/23/2019/06/LibraWhitePaper_en_US.pdf)

[^5]:
     [https://globalfindex.worldbank.org/](https://globalfindex.worldbank.org/)

[^6]:
    [https://www.fdic.gov/householdsurvey/](https://www.fdic.gov/householdsurvey/)

[^7]:
     [https://slideslive.com/38920018/living-on-defi-how-i-survive-argentinas-50-inflation](https://slideslive.com/38920018/living-on-defi-how-i-survive-argentinas-50-inflation)

[^8]:
     [https://www.coindesk.com/oxfam-trials-delivery-of-disaster-relief-using-ethereum-stablecoin-dai](https://www.coindesk.com/oxfam-trials-delivery-of-disaster-relief-using-ethereum-stablecoin-dai)


<!-- Docs to Markdown version 1.0β17 -->
