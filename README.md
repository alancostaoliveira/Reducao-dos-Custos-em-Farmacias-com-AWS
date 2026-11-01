🚀 Relatório de Implementação de Serviços AWS: Otimização de Custos
<p align="center">
  <img src="https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white" alt="AWS"/>
  <img src="https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen?style=for-the-badge" alt="Status"/>
  <img src="https://img.shields.io/badge/Empresa-Abstergo%20Industries-blue?style=for-the-badge" alt="Empresa"/>
</p>
---
📌 Informações Gerais
Item	Detalhes
Empresa	Abstergo Industries
Responsável Técnico	Alan Costa de Oliveira
Data de Implementação	01 de Novembro de 2026
Objetivo Principal	Redução imediata de custos de infraestrutura e otimização operacionais via AWS
---
📝 Introdução
Este documento apresenta a documentação técnica da implementação de soluções da Amazon Web Services (AWS) realizada na Abstergo Industries. O objetivo central do projeto consistiu na identificação, arquitetura e execução de 3 serviços estratégicos focados na eliminação de desperdícios de recursos, otimização de computação e gestão inteligente de dados, visando uma diminuição drástica nos custos da fatura de nuvem.
---
🏗️ Descrição do Projeto e Etapas de Implementação
O projeto foi dividido em três etapas estratégicas, cobrindo as camadas de Computação, Armazenamento e Elasticidade Dinâmica.
```
    ┌────────────────────────────────────────────────────────┐
    │              Redução de Custos AWS                     │
    └───────────────────┬────────────────────────────────────┘
                        │
      ┌─────────────────┼─────────────────┐
      ▼                 ▼                 ▼
 ┌──────────┐     ┌──────────┐     ┌─────────────┐
 │ EC2 Spot │     │ S3/Glacier│     │Auto Scaling │
 └──────────┘     └──────────┘     └─────────────┘
 (Computação)    (Armazenamento)   (Elasticidade)
```
---
🔹 Etapa 1: Computação Otimizada com Amazon EC2 Spot Instances
Ferramenta: Amazon EC2 Spot Instances
Foco: Otimização severa de custos em processamento de dados e ambientes não críticos/homologação.
Caso de Uso: Migração de cargas de trabalho tolerantes a falhas, pipelines de CI/CD, testes de integração e processamentos em lote (batch processing) para instâncias Spot. Essa estratégia permitiu utilizar a capacidade ociosa da AWS com descontos de até 90% em comparação às instâncias sob demanda (On-Demand).
---
🔹 Etapa 2: Gestão de Ciclo de Vida de Dados no Amazon S3
Ferramenta: Amazon S3 Lifecycle Policies & S3 Glacier
Foco: Automação do ciclo de vida de arquivos e armazenamento de longo prazo de baixo custo.
Caso de Uso: Implementação de políticas de ciclo de vida (Lifecycle Rules) para transição automática de logs de aplicações, métricas e backups.
30 dias: Migração do S3 Standard para S3 Glacier Flexible Retriever.
90 dias: Transição para S3 Glacier Deep Archive, reduzindo o custo por GB armazenado ao valor mínimo possível da infraestrutura.
---
🔹 Etapa 3: Elasticidade e Desligamento Programado com AWS Auto Scaling
Ferramenta: AWS Auto Scaling & EventBridge
Foco: Dimensionamento dinâmico baseado na demanda real e desligamento automático de ambientes ociosos.
Caso de Uso:
Configuração de políticas de escalamento (Target Tracking) ajustadas ao uso real de CPU e tráfego de rede.
Implementação de rotinas automatizadas para desligar 100% dos ambientes de desenvolvimento e testes fora do horário comercial (noites e fins de semana), eliminando cobranças desnecessárias de recursos ociosos.
---
📊 Tabela Comparativa de Economia
Serviço	Abordagem Anterior	Nova Abordagem (Implementada)	Economia Estimada
Computação	EC2 On-Demand 24/7	EC2 Spot + Desligamento Programado	~75%
Armazenamento	S3 Standard permanente	S3 Standard + S3 Glacier Deep Archive	~80%
Escalabilidade	Instâncias provisionadas fixas	AWS Auto Scaling Dinâmico	~40%
Geral (Fatura AWS)	Recursos sem otimização	Arquitetura Enxuta e Automatizada	~60% Total
---
🎯 Conclusão
A implementação dos serviços AWS na Abstergo Industries garantiu uma redução imediata e sustentável nos custos operacionais da infraestrutura em nuvem. Ao combater a subutilização e aplicar políticas automáticas de gerenciamento, a empresa atingiu um nível superior de eficiência operacional e sustentabilidade financeira, estimando uma redução global de até 60% na fatura mensal da AWS.
Recomendações:
Acompanhamento diário dos custos através do AWS Cost Explorer e criação de alertas de orçamento via AWS Budgets.
Avaliação contínua para inclusão de AWS Savings Plans para cargas de trabalho de produção ininterruptas.
---
📎 Anexos e Automações
<details>
<summary>📂 <b>Anexo 1: Configuração da Política de Ciclo de Vida do S3 (JSON)</b></summary>
```json
{
  "Rules": [
    {
      "ID": "MoverLogsEBackupsParaGlacier",
      "Status": "Enabled",
      "Filter": {
        "Prefix": "logs/"
      },
      "Transitions": [
        {
          "Days": 30,
          "StorageClass": "GLACIER"
        },
        {
          "Days": 90,
          "StorageClass": "DEEP_ARCHIVE"
        }
      ]
    }
  ]
}
```
</details>
<details>
<summary>📂 <b>Anexo 2: Script AWS CLI para Parada de Instâncias Ociosas (Dev/Homolog)</b></summary>
```bash
#!/bin/bash
# Desliga instâncias com a tag Environment=Development
aws ec2 stop-instances --instance-ids $(aws ec2 describe-instances \
  --filters "Name=tag:Environment,Values=Development" "Name=instance-state-name,Values=running" \
  --query "Reservations[*].Instances[*].InstanceId" \
  --output text)
```
</details>
---
<p align="center">
  <b>Alan Costa de Oliveira</b><br>
  <i>Engenheiro de Cloud / Responsável pelo Projeto</i>
</p>
