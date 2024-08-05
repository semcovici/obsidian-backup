Existem diversas maneiras de modelos de IA generativa consultar dados estruturados. Quando estamos lidando com bases pequenas, podemos apenas transformar nossas tabelas em vetores e armazenar em algum banco de vetores. Já quando estamos trabalhando com bases de dados grande, se torna bem mais difícil utilizar estratégias como essa e precisamos utilizar estratégias baseadas em Text2SQL, onde pedimos para uma LLM criar um query SQL que selecione os dados que precisamos e depois continuamos o processo.

## Text2SQL

### create_sql_agent langchain
Uma estratégia mais simples é utilizar algum agente pronto do langchain para realizar a tarefa. Um dos que achei foi o create_sql_agent, que foi bastante problemático em meus testes e optei por não dar continuidade.

https://www.datascienceengineer.com/blog/post-chat-with-bigquery

### Solução Simples

Abaixo há uma solução simples de Text2SQL;
[Open source framework for connecting LLMs to your data | Google Cloud Blog](https://cloud.google.com/blog/products/ai-machine-learning/open-source-framework-for-connecting-llms-to-your-data)
Abaixo há uma solução um pouco mais incrementada da de cima, mas ainda segue a mesma lógica.

https://colab.research.google.com/drive/1vL8QYCj42uQrMRkCbCvGOemQgmcnygqj?usp=sharing#scrollTo=TA4nJ2OTP8ej
https://medium.com/google-cloud/write-sql-with-natural-language-using-vertex-ai-and-bigquery-c849559f8a5f
### Opendataqna
Uma solução bastante robusta de Text2SQL [GoogleCloudPlatform/applied-ai-engineering-samples at opendataqna (github.com)](https://github.com/GoogleCloudPlatform/applied-ai-engineering-samples/tree/opendataqna "https://github.com/googlecloudplatform/applied-ai-engineering-samples/tree/opendataqna")


## Function Calling

Utilizando fuction calling ([Function calling  |  Generative AI on Vertex AI  |  Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/multimodal/function-calling "https://cloud.google.com/vertex-ai/generative-ai/docs/multimodal/function-calling")). Nessa a gente criaria querys que os usuários fariam e a llm só chamaria uma função que faz aquela query no bq e depois retornaria o resultado pro usuário. Essa solução é boa caso a gente perceba que existem querys parecidas que os usuários fazem, pq a gente generaliza aquela query em uma função e a llm só preenche os parâmetros. Dessa forma, evita ao máximo alucinação.

## Utilizar vector store

utilizar o esquema parecido com e-commerce de criar um json (objeto) que represente cada entidade, no nosso caso seriam os candidatos ou partidos por exemplo, e fazer a busca em cima dos json no vertex search. Essa solução me pareceu um pouco ruim e com altas tendencias de alucinação, inclusive o afonso foi mostrar para a gente dois exemplos e nos dois as respostas foram um pouco imprecisas kkk