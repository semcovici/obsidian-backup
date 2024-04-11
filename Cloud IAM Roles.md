Roles são o "What" do [[GCP Cloud IAM]]. Ou seja, ele define quais [[Cloud IAM Permissions]] tem o usuário ou membro que possui esse role. Em poucas palavras, **Roles são uma coleção de Permissions**.

Existem 3 tipos de roles:
* Owner: tem 100% de acesso as configurações do recurso
* Editor: consegue modificar um role e adicionar novas permissões
* Viewer: apenas consegue ver as permissões

Todo recurso do GCP tem roles pré-definidos que facilitam a configuração. Porém, se os roles pré definidos não satizfazer o propósito, pode-se criar roles customizados.

