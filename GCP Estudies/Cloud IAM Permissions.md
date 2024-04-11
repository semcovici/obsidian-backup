Determinam as operações possíveis em um recurso à um certo [[GCP Estudies/Cloud IAM Roles]]. Ou seja, determinam o que cada Role pode fazer em um determinado recurso.

Não é posssível dar uma permissão para um member ou user, apenas a um role.

As permisões seguem o formato:
```<service>.<resource>.<verb>```
Exemplos:
- pubsub.subscriptions.consume
- compute.instances.inset