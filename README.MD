# Treinamento

## Divisão em camadas

- Divido em algumas camads:
  - Apresentação
  - Aplicação
  - Domínio
  - Infraestrutura

## Objetos de Valor
- Uma coisa que não tem um atributo que define algo único, exemplos:
  - Posso ter um objeto de valor CPF, Email, Telefone;
  - Adiciono lógica em cima do objeto de valor;

## Building Blocks

- Entity
- Value Object
- Repository
- Factory
- Service


## Linguagem ubíque
- Linguagem universal entre área de negócio e time técnico;
- Preciso ter no código os termos falados no domínio;


## Invariante
- Uma regra de negócio em cima da minha entidade - value object

## Aggregate
- Aggregate são classes que mantém outras classes, caso da classe aluno ter telefone, e-mail e cpf;
- Tu vai fazer as manipulações dentro da classe aggregate, exemplo, vou adicionar uma validação de quantidade de telefone dentro do agreggate.
- https://martinfowler.com/bliki/DDD_Aggregate.html
- Persistência:
  - Como salvo as questões das diferentes classes?
  - Salvo tudo junto na aggregate;
  - Evitar repositório para as classes de object value;
  - Garanto que não terei inconsistência;

## Eventos
- Um evento é algo que aconteceu, e algum processamento precisa acontecer, podendo ser um ou mais ouvintes para fazer o processamento;
- Tenho um interface comum para eventos;
- Preciso ter o tempo que aconteceu;
- E preciso enviar uma informação relevante sobre o evento;
  - Nem sempre faz sentido passar a classe inteira;
  - Muitas vezes é melhor passar só um dado da classe;

### Ouvintes
- Classe que vai ser chamada quando o evento for disparado;
- Vou ter uma classe abstrata ouvinte, que vai lidar com o Reage e também verificar se deve reagir;
- Vou extender nos meus ouvintes essa classe abstrata;


### Publicador de eventos
- Tenho uma classe que publica todos eventos;
- Tenho os registros da minha lista de ouvintes;
- Disparo o evento na minha use case;

## Contextos Delimitados
- Separação de contextos por pacotes;
- Mas posso separar em diferentes maneiras;
- Vou ter pacotes macros:
  - Vão se módulos diferentes;
  - Cada um com suas camadas;
- Preciso cuidar com acoplamento;
  - Se eu tenho acoplamento das classes de domínio do módulo 1 com as do módulo 2, não faz muito sentido separar
  - Uso de mapas de contextos;
    - Vejo todos os contextos;
    - Vejo como são as relações entre contextos;
    - Tenho um núcleo compartilhado;

- Como faço a comunicação entre módulos?
  - Através de shared kernel;
    - Mais acoplamento;
  
  - Ou através da duplicação de código;
    - Mais desacoplamento;
    - Mas tenho duplicação de código;

- https://martinfowler.com/bliki/BoundedContext.html

## Shared Kernel

- Compartilhamos um contexto compartilhado;
- Um pacote que vai representar as classes que são compartilhadas;
- Dentro do pacote (módulo) vai ter um pacote domínio;
- https://maiconheck.medium.com/domain-driven-design-os-building-blocks-parte-3-domain-subdomains-e-bounded-contexts-a51d5a9d9851

### Como vou gerar um evento global?
- Preciso compartilhar as classes Eventos, Ouvintes e Publicadores;

- Problema o que acontece se meu evento pertence a outro contexto?
  - Várias abordagens;
  - Uma delas é passar para o contexto shared, os tipos de eventos;
    - Podendo ele ser um enum;

- Como acesso infos específicas do evento sem acessar o domínio de outro módulo?
  - Posso retornar um mapa no evento com "informações";
  - Assim, deixo genérico;
  - Eu mesmo vou acessar as informações

## Sistemas Distribuídos
