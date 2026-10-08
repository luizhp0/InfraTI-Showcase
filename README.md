<div align="center">

# InfraTI

### Mapeamento interativo e gestão de infraestrutura de TI

**Transformando informações técnicas em uma visão clara da infraestrutura.**

![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-181818?style=flat-square&logo=supabase&logoColor=3FCF8E)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)

**Projeto de uso interno · Repositório de apresentação (showcase)**

</div>

---

## Sobre o projeto

O **InfraTI** é um sistema web desenvolvido para organizar e acompanhar a infraestrutura de tecnologia da informação diretamente em uma **planta interativa em 2D**.

A ideia nasceu de uma necessidade prática: conseguir localizar equipamentos, pontos de rede e ambientes de maneira rápida, sem depender de informações espalhadas em diferentes registros.

Com o mapa, é possível visualizar a distribuição dos recursos, acompanhar o andamento das instalações e consultar detalhes de cada item. O sistema também conta com uma ferramenta para **estimar a cobertura Wi-Fi**, auxiliando no planejamento da posição dos pontos de acesso.

## Principais funcionalidades

| Recurso | O que faz |
| --- | --- |
| **Mapa interativo** | Navegação pela planta com zoom, deslocamento e seleção de ambientes |
| **Pontos de rede** | Cadastro, posicionamento e acompanhamento dos estados: pendente, instalado e funcionando |
| **Equipamentos** | Registro e movimentação de computadores, impressoras, switches, servidores e dispositivos de rede |
| **Fichas técnicas** | Organização de dados dos ativos, como identificação, ambiente e observações |
| **Pesquisa** | Localização de equipamentos e pontos no mapa, com apoio à identificação de IPs duplicados |
| **Camadas e filtros** | Exibição de categorias específicas e filtragem por status |
| **Persistência e histórico** | Armazenamento dos registros, controle de permissões e rastreabilidade das alterações |
| **Cobertura Wi-Fi** | Estimativa visual de sinal para comparar posições de pontos de acesso |

---

## Simulação de cobertura Wi-Fi

Um dos recursos que mais gosto no InfraTI é a **visualização estimada da cobertura Wi-Fi sobre a própria planta**.

Em vez de posicionar os equipamentos apenas por tentativa e erro, o sistema permite comparar diferentes locais de instalação e identificar regiões que *podem* apresentar cobertura insuficiente.

### Como funciona na prática

1. No perfil de administrador, é possível selecionar ou posicionar um ponto de acesso compatível no mapa.
2. A planta é calibrada a partir de uma distância real conhecida, convertendo medidas do desenho para metros.
3. O sistema calcula uma estimativa do sinal em diferentes regiões, considerando a **distância até o equipamento** e as **paredes atravessadas**.
4. O resultado aparece como uma área colorida na planta. Ao movimentar o equipamento, a estimativa é recalculada, permitindo comparar posições.

A visualização utiliza cinco faixas: **muito bom, bom, aceitável, fraco e sem cobertura útil estimada**.

### A lógica por trás da estimativa

A implementação atual utiliza um modelo simplificado de perda de sinal:

```text
Sinal estimado = -40 - 22 × log10(distância em metros) - (5 × paredes)
```

- **-40:** valor de referência assumido a 1 metro, não uma medição do equipamento.
- **22 × log10(distância):** redução estimada conforme a distância aumenta; distâncias abaixo de 1 metro são tratadas como 1 metro.
- **5 × paredes:** penalidade padrão por parede atravessada entre o ponto de acesso e a região analisada.

O sistema traça o caminho entre o equipamento e cada ponto de uma grade de cálculo, verifica os cruzamentos com as paredes e transforma o resultado em uma representação visual.

Por exemplo, **a 10 metros** do ponto de acesso:

| Cenário | Valor estimado |
| --- | ---: |
| Sem paredes | -62 |
| Com 1 parede | -67 |
| Com 2 paredes | -72 |
| Com 3 paredes | -77 |

> **Limitações do modelo:** a simulação é uma ferramenta de apoio ao planejamento, não uma medição real de sinal ou velocidade. Interferências, materiais de construção, características dos dispositivos e condições do ambiente influenciam a cobertura. Os perfis de equipamentos atualmente compartilham os mesmos parâmetros de cálculo; a calibração com medições reais é uma possível evolução do projeto.

Essa funcionalidade une **visualização espacial, geometria e lógica de cálculo** a uma necessidade real de infraestrutura.

---

## Tecnologias utilizadas

| Tecnologia | Aplicação no projeto |
| --- | --- |
| **React** | Interface e componentes interativos |
| **TypeScript** | Lógica da aplicação e tipagem |
| **Supabase** | Serviços de dados, autenticação e integração |
| **PostgreSQL** | Armazenamento das informações |
| **Vercel** | Publicação da aplicação web |

### Perfis de acesso

O sistema separa as permissões por perfil. **Administradores** podem gerenciar informações, editar o mapa e utilizar ferramentas de planejamento, enquanto **visitantes** têm acesso de consulta às visualizações permitidas.

As alterações são persistidas no banco de dados e o sistema mantém registros para acompanhamento e auditoria.

## Desafios de desenvolvimento

Durante a construção do InfraTI, precisei trabalhar com problemas que vão além de telas e formulários:

- Representar ambientes e ativos técnicos de maneira intuitiva em um mapa 2D.
- Permitir a interação com elementos posicionados espacialmente, incluindo zoom e movimentação.
- Integrar os dados do mapa ao armazenamento persistente e às permissões dos usuários.
- Construir uma estimativa de cobertura que considera distâncias reais e cruzamentos com paredes.
- Organizar funcionalidades de consulta e edição sem deixar a interface complicada.

## Meu papel no projeto

Fui responsável pelo desenvolvimento da aplicação, trabalhando na interface, nas interações do mapa, na integração com os dados e na implementação das funcionalidades de gerenciamento e planejamento.

O InfraTI reúne duas áreas com as quais tenho contato no dia a dia: **infraestrutura de TI e desenvolvimento de software**.

## Imagens do sistema

**Galeria em preparação.** As capturas de tela serão incluídas após revisão e autorização para divulgação, com informações institucionais sensíveis removidas ou substituídas.

A apresentação visual deverá mostrar:

- A interface geral e a navegação pelo mapa.
- O cadastro e o posicionamento de tipos de equipamentos.
- A visualização da cobertura Wi-Fi estimada, em uma **planta demonstrativa ou devidamente autorizada**, sem revelar o layout real e a localização dos ativos de rede.

## Por que o código não está disponível?

O InfraTI foi desenvolvido para uso interno. Por isso, **o código-fonte, os dados operacionais e o acesso à aplicação não são públicos**.

Este repositório existe exclusivamente para apresentar o projeto, seus objetivos, desafios de desenvolvimento e tecnologias utilizadas, respeitando a confidencialidade das informações institucionais.

---

<div align="center">

**Desenvolvido por [Luiz Henrique de Pieri](https://github.com/luizhp0)**

[LinkedIn](https://www.linkedin.com/in/luizhenriquedepieri) • [Contato](mailto:oficialluizff@gmail.com)

</div>
