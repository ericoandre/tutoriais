# Crie uma conta de administrador

O princípio de menor privilégio é um conceito de segurança bem conhecido que limita o acesso de um usuário apenas ao que é necessário para realizar seu trabalho. 

As credenciais do usuário raiz oferecem acesso ilimitado a uma conta e a todos os seus recursos. Com isso em mente, é fácil ver por que o acesso raiz raramente é necessário. Em vez disso, você deve usar usuários de gerenciamento de identidade e acesso (IAM) e funções do IAM com permissões restritas.


## Como adicionar um administrador: 

1. Faça login em sua conta da AWS usando suas credenciais de usuário raiz. 
2. **Utilize grupos para dar permissões.** Ao menos um grupo precisa ser criado, vamos criar um grupo que terá acesso full, acesso de Administrador (root) a esta conta, para isso siga os abaixo. Vá em Groups - Create New Group.<p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/blob/main/aws/aws.png"/></p>
3.  Defina um nome para o Grupo. No exemplo, está Admins, pois este grupo terá acesso full na conta.<p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/blob/main/aws/NomeGroup.png"/></p>
4. Adicione policies para este grupo. A policy que dá acesso full a conta é a AdministratorAccess. Dessa forma podemos vincular ao menos um usuário a este grupo e ao invés de utilizar o root para acessar a conta (conforme boas práticas), utilizaremos este novo usuário que será criado no segundo passo.<p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/blob/main/aws/AddPolicyGroup-1.png"/></p>
5. Revise e crie o grupo.<p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/blob/main/aws/ReviewGroup-Create.png"/></p>

Feito isso, já podemos partir para o segundo passo, criar ao menos um usuário e vincular a este grupo, para não utilizarmos mais o root no dia a dia.



1. **Crie usuários.** Um usuário com acesso de administrador precisa ser criado para que a conta root não seja utilizada nas tarefas diárias, para isso siga os passos abaixo. Vá em Users - Add user. <p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/blob/main/aws/Menu-User.png"/></p>
2. Escolha o nome do usuário. Como esse usuário irá fazer o papel de Admin da conta, você pode marcar os dois tipos de acesso, via acesso programático (permite que você utilize as credenciais de acesso - Access Key ID e Secret access Key - para acessar a AWS) e via console, já coloque uma senha forte e assim não será necessário alterar depois. <p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/\aws/Captura de Tela (2).png"/></p>
3. Vincule o usuário a um grupo. Ou escolha outras opções de acordo com a necessidade. Aqui vamos vincular o usuário ao grupo Admins recém criados. <p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/blob/main/aws/User-step2.png"/></p>
4. Adicione Tags ao usuário. Este item é opcional e vamos deixá-lo em branco, mas ele serve para identificar e/ou separar os recursos AWS, ele utiliza o conceito chave:valor. Por exemplo, queremos separar usuários, máquinas, buckets utilizadas pelo departamento Financeiro da empresa dos itens do departamento Fiscal, poderíamos colocar Departamento: Financeiro ou Departamento: Fiscal, de acordo com o uso/criação. <p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/blob/main/aws/User-step3.png"/></p>
5. Revisar as informações e criar o usuário.<p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/blob/main/aws/User-step4.png"/></p>
6. Usuário criado, e ele traz as informações de acesso para este usuário, como: URL para acessar o console, afinal não utilizaremos mais a opção Root user e sim IAM user, e caso não utilize a url fornecida nesse momento, você precisará saber o ID da conta do root. Além disso, também é fornecido o Access Key ID e Secret access Key desse usuário.<p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/blob/main/aws/user-step5.png"/></p>

**Importante:** Faça o Download do .csv ou salve a Access Key ID e Secret access Key ou envie por e-mail, pois essa será a única vez que poderá visualizar essa informação.



**IAM Roles** - O conceito é bem similar ao de IAM Users, Roles é um conjunto de policies que permitem o acesso aos recursos da AWS, podendo executar n funções, só que ao invés de ser vinculado a apenas uma pessoa, várias podem ter acesso. Além disso, ele é um acesso temporário ou especifico para um dado recurso ou situação, ele pode ser facilmente vinculado/desvinculado de um recurso ou conta. Exemplo fictício fora do mundo AWS: Essa empresa criou um conjunto de regras, que em determinado período você pode acessar a pasta Contabilidade e realizar consultas e alterações em alguns documentos e pastas.

**IAM Groups** - É outro conceito simples, determinado usuário pertence a um grupo de pessoas que podem ter acessos a determinadas coisas na empresa. Exemplo fictício fora do mundo AWS: Ainda pensando na sua contratação na empresa, você é do departamento do Financeiro e aquele usuário que você acessou o computador vai estar no grupo Financeiro e vai poder acessar as pastas ContasPagar e ContasReceber na rede.

**IAM Policies** - É o item mais granular de permissões na AWS. Aqui você vai poder dizer que determinado recurso pode ou não executar uma ou mais ações. Por exemplo, podemos definir uma policy onde se tenha apenas o acesso de start e stop de instâncias EC2. Exemplo fictício fora do mundo AWS: Continue a pensar na sua contratação, o seu usuário está em apenas no grupo Financeiro, mas também está vinculado a uma policy que permite que você acesse para visualizar um determinado arquivo na pasta Faturamento, mas não tenha acesso de copiar nem modificar este arquivo.



## Criar uma instância do Amazon SageMaker Notebook

Uma instância de SageMaker notebook da Amazon é uma instância de computação totalmente gerenciada de aprendizado de máquina (ML) do Amazon Elastic Compute Cloud (Amazon EC2)  fornece ambientes de computação virtual capacidade escalável, que executa o aplicativo Jupyter Notebook. Você usa a instância do notebook para criar e gerenciar notebooks Jupyter para pré-processamento de dados e para treinar e implantar modelos de aprendizado de máquina.

<p align="center"><img alt="" src="https://github.com/ericoandre/tutoriais/blob/main/aws/gs-ni-create-instance.gif"/></p>

1. Abra o SageMaker console da Amazon em https://console.aws.amazon.com/sagemaker/.
2. Escolha **Instâncias do Notebook** e, em seguida, escolha **Create notebook instance**.
3. Na página **Create notebook instance (Criar instância de bloco de anotações)**, forneça as seguintes informações (se um campo não for mencionado, deixe os valores padrão):
   1. Em **Notebook instance name (Nome da instância de bloco de anotações)**, digite um nome para a sua instância de bloco de anotações.
   2. Em **Notebook Instance type (Tipo de instância de bloco de anotações)**, escolha `ml.t2.medium`. Esse é o tipo de instância mais barato com suporte das instâncias do bloco de anotações, e é suficiente para este exercício. Se um tipo de `ml.t2.medium` instância não estiver disponível em sua AWS região atual, escolha `ml.t3.medium`.
   3. Em **Identificador de plataforma**, escolha um tipo de plataforma na qual criar a instância do notebook. Esse tipo de plataforma determina o sistema operacional e a JupyterLab versão com a qual sua instância de notebook é criada. Para obter informações sobre o tipo de identificador de plataforma, consulte [Amazon Linux 2 versus instâncias de notebook Amazon Linux](https://docs.aws.amazon.com/pt_br/sagemaker/latest/dg/nbi-al2.html). Para obter mais informações sobre as versões do JupyterLab, consulte [JupyterLabcontrole de versão](https://docs.aws.amazon.com/pt_br/sagemaker/latest/dg/nbi-jl.html).
   4. Para a **função do IAM**, escolha **Criar uma nova função** e, em seguida, escolha **Criar função**. Essa função do IAM obtém automaticamente permissões para acessar qualquer bucket do S3 que tenha `sagemaker` no nome. Ela obtém essas permissões por meio da política `AmazonSageMakerFullAccess`, que o SageMaker anexa à função.
   5. Escolha **Create notebook instance** (Criar instância de **notebook**).

Em alguns minutos, SageMaker inicia uma instância de computação de ML — nesse caso, uma instância de notebook — e anexa a ela um volume de armazenamento de 5 GB do Amazon EBS. A instância do notebook tem um servidor de notebook Jupyter pré-configurado, bibliotecas AWS SDK SageMaker e um conjunto de bibliotecas Anaconda.

Para obter mais informações sobre como criar uma instância de SageMaker notebook, consulte [Criar uma instância de notebook](https://docs.aws.amazon.com/sagemaker/latest/dg/howitworks-create-ws.html).

