🔄 Integração com GitHub
✅ Passos para conectar o repositório GitHub ao Azure
No Azure Databricks, acesse User Settings > Git Integration.

Selecione o Git provider (GitHub).

Cole seu token pessoal do GitHub.

Clone o repositório no ambiente do Databricks ou sincronize os notebooks diretamente com a branch desejada.



🔄 Integração com Azure DevOps
✅ Passos para configurar Azure Repos como controle de versão
Crie um novo projeto no Azure DevOps.

Configure o repositório (Repos) para armazenar os notebooks exportados.

Utilize a CLI do Databricks ou automações para exportar os notebooks para o repositório.



💡 Boas Práticas de Versionamento
Commitar notebooks com frequência.

Utilizar branches para funcionalidades específicas.

Adotar convenções claras de nomeação (feature/, bugfix/, hotfix/).

Sempre abrir Pull Requests com revisões antes do merge.



♻️ Backups Automatizados
Exemplo de Pipeline YAML para Backup
yaml
Copiar
Editar
trigger:
  schedule:
    - cron: "0 2 * * *"
      displayName: 'Daily Backup'
      branches:
        include:
          - main

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: UsePythonVersion@0
  inputs:
    versionSpec: '3.x'

- script: |
    pip install databricks-cli
    databricks workspace export_dir /Workspace/Users/usuario@empresa.com /mnt/backup/notebooks --overwrite
  displayName: 'Exportar notebooks do Databricks'


☁️ Armazenamento de Backups
Os notebooks exportados são armazenados em:

Azure Repos (branch de backup)

Blob Storage (opcional)

GitHub backup branch (opcional)

🔒 Segurança
Armazenar tokens e secrets no Azure Key Vault.

Usar pipelines protegidas com acesso limitado.

Proteger branches principais com regras de aprovação.

📈 Histórico e Auditoria
Todo o histórico de alterações pode ser consultado via:

Histórico de commits no GitHub/Azure Repos

Logs de execução dos pipelines

Auditoria de acessos no Azure

✅ Exemplo de Fluxo Completo
Desenvolvedor edita notebook no Databricks.

Realiza commit e push via integração Git.

Pipeline realiza backup diário dos notebooks.

Pull Requests garantem revisão de código e versionamento.
