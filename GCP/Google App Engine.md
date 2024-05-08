Um serviço oferecido pelo  [[Google Cloud Platform (GCP)]] como um dos [[GCP Compute Services]]

The Simplest way to deply and scale one app in GCP.
* Provides end-to-end application management

**Features:**
* Automatic lb & auto scaling 
* Manged platform updates & application health monitoring 
* application versioning
* traffic splitting


* Compute service do Google (PaaS)
* Deploy de aplicações web que escalam (aumentam ou diminuem o tamanho de acordo com a demanda)
* suporta multiplas linguagens, frameworks e bibliotecas 

### Enviroments
<u>Standard</u>:
* complete isolation from OS/Disk
* Supports scale down to Zero instances

mais fácil e rápido de fazer o deploy e escalar a aplicação, mas possui limitações em relação a linguagem e bibliotecas

**<u>Flexible</u>:
* Makes use of [[Google Compute Engine (GCE)]] VMs
* Support ANY runtime
* CANNOT scale down to Zero instances

roda containers, então dá pra rodar praticamente qualquer coisa. Porém, demora mais para realizar o deploy e, geralmente, é mais caro.