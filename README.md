# Pipeline ETL Serverless para Simulação de Datalake na AWS – Glue + S3 + Athena

## 🎥 Vídeo Demonstrativo  
Para ver todo o processo do projeto em ação, assista ao vídeo explicativo:  
👉 [Clique aqui para assistir ao vídeo no youtube](https://www.youtube.com/watch?v=GXAscrgeP4c) 


---

## 📌 Descrição do Projeto  
Este projeto demonstra um fluxo completo de **pipeline ETL serverless** utilizando **AWS Glue**, **Amazon S3** e **Amazon Athena**, com o objetivo de simular um **datalake**.  
O projeto simula uma arquitetura típica de datalake, onde dados brutos e dados tratados ficam organizados em camadas distintas no S3, e um pipeline ETL processa e integra os dados para análises eficientes.

---

## 🛠 Arquitetura  
O fluxo foi projetado para ser totalmente **serverless**, ou seja, sem necessidade de provisionar ou gerenciar servidores, aproveitando serviços gerenciados da AWS.

**Fluxo resumido:**  
1. **Armazenamento de dados brutos** no S3 (`sourcedata`) — camada raw do datalake  
2. **Catalogação** dos arquivos no **AWS Glue Data Catalog** via **Crawler**  
3. **Transformação** no **Glue Studio** (joins, desnormalização, limpeza) — ETL Jobs  
4. **Carga** do resultado final no S3 (`datalake`) em formato Parquet e **particionado** — camada curated do datalake  
5. **Consulta otimizada** no Athena

---

## 📂 Estrutura do Projeto no S3  
/sourcedata
* clientes_csv.csv
* vendedores_csv.csv
* produtos_csv.csv
* vendas_csv.csv
* itensvenda_csv.csv

/datalake
* status_vendedor=Gold/...
* status_vendedor=Silver/...
* status_vendedor=Platinum/...

/logs

/scripts

/temp

## 🔄 Processo de ETL  
### 1️⃣ Extração  
- Os arquivos originais (clientes, vendedores, produtos, vendas e itens de venda) foram carregados na pasta `sourcedata` no S3.

### 2️⃣ Transformação  
No **AWS Glue Studio**, foram realizadas as seguintes etapas:  
- **Desnormalização**: unificação de todas as tabelas em um único dataset.  
- **Joins**: integrando vendas com clientes, vendedores, produtos e itens de venda.  
- **Renomeação de colunas**: para evitar conflitos de nomes iguais.  
- **Remoção de colunas desnecessárias**: limpeza para melhorar performance e reduzir custo.  
- **Particionamento**: separação por `status_vendedor` para otimizar consultas.

### 3️⃣ Carga  
- O dataset final foi salvo no formato **Parquet**, já **particionado**, na pasta `datalake` do S3.

## 📁 Estrutura do Repositório  
/evidencias
- prints_s3.png
- prints_glue_crawler.png
- prints_glue_studio.png
- prints_athena.png

/sourcedata
- clientes_csv.csv
- vendedores_csv.csv
- produtos_csv.csv
- vendas_csv.csv
- itensvenda_csv.csv

---

## 🔐 IAM Role  
- Foi criado um **IAM Role** que concede as permissões necessárias para que o Glue acesse os buckets do S3, execute crawlers e jobs com segurança.  
- Isso garante que apenas serviços autorizados possam acessar ou modificar os dados.

---

## 🚀 Tecnologias Utilizadas  
- **AWS S3** – Armazenamento de dados brutos e tratados  
- **AWS Glue** – ETL serverless e Data Catalog  
- **AWS Glue Studio** – Transformações visuais  (ETL Jobs)
- **AWS Athena** – Consulta SQL serverless sobre dados no S3  
- **Parquet** – Formato otimizado para consulta e armazenamento

---

## 📬 Contato

- [LinkedIn](https://www.linkedin.com/in/kauansilva96/)
- [Biolink](https://biolink.website/socialKauanSilva)
- Email: kauangsilva1996@gmail.com

