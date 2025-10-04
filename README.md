# baiters-burger-database

## Visão geral
Nesta fase do projeto decidimos migrar o banco de dados de MongoDB para o AWS RDS MySQL, primeiro porque queríamos um banco de dados auto-gerenciado com um custo baixo e com pouco requisito computacional, pois não temos dimensão o suficiente para saber como será preciso escalar o banco ainda, se vamos escalar verticalmente ou horizontalmente, a princípio setamos uma instancia db.t3.micro com alertas de performance com um SNS para avisar por e-mail, e assim analisar os dados para nos basearmos se continuamos com um RDS MySQL, se continuaremos com relacional ou talvez até migrar para um Amazon Aurora, dependendo da necessidade. 

Dito isso aqui estão nossos modelos de dados.

- Modelo concentual:
[ alt text](/doc/images/conceptual-model.png)

- Modelo lógico:
[ alt text](/doc/images/logical-model.png)

- Modelo físico:
[ alt text](/doc/images/physical-model.png)



## Pré-requisitos
Para criação da infraestrutura como código você precisará de algumas pré configurações:
- instalação do terraform: https://developer.hashicorp.com/terraform/install
- instalação do aws cli e/ou apenas uma .aws/credentials com a devida configuração das credenciais:
    https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html 
    https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html


## Informações técnicas:
- Engine: MySQL 8.x
- Região: us-east-1
- Acesso: público (apenas para desenvolvimento) via SG rds-public-sg
- VPC: default
- Subnets: default (db subnet group)
- Security Group: 3306/tcp (ajuste para faixas internas)
- Alarms: CPU >= 70% (SNS rds-alerts-topic)