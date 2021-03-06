---

copyright:
  years: 2016

---

#	Usando o plano Developer
{: #using_mobilefoundation_p1}

Última atualização: 4 de agosto de 2016
{: .last-updated}

Após criar a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Desenvolvedor, em alguns segundos, será possível acessar a página `Visão geral`
no {{site.data.keyword.Bluemix_notm}}, que fornece tutoriais e vídeos para ajudá-lo a
iniciar o serviço {{site.data.keyword.mobilefoundation_short}}.

## Iniciando o servidor {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p1}
* Para iniciar o {{site.data.keyword.mfserver_short_notm}} com configurações padrão, clique em **Iniciar servidor básico**.

Esta seleção provisiona um {{site.data.keyword.mfserver_long_notm}} com as configurações a seguir:
*	1 GB de memória. Este tamanho é suficiente para desenvolvimento, atividades de teste leve e cargas de trabalho de produção em pequena escala.

*	O `username` e a `password` são gerados automaticamente para
você. Você tem acesso a eles quando o servidor está funcionando.

O processo de fornecimento inicia. Esse processo leva aproximadamente 10 minutos e uma
janela de mensagem indica o progresso dessa operação. Quando completo, um painel é exibido
no qual é possível ver:
*	O status do servidor que está em execução (estado, tamanho).

*	A rota do servidor criada para você. Use esta rota em seu aplicativo móvel para se
conectar ao {{site.data.keyword.mfserver_short_notm}}.

*	Seu `nome do usuário` e `senha` para acessar o {{site.data.keyword.mfp_oc_short_notm}}. A `password` fica oculta. Clique
no ícone **Mostrar senha** para visualizá-lo.

*	Clique em **Ativar console** para ativar o {{site.data.keyword.mfp_oc_short_notm}}.


<!--This console runs inside the container.--> Com o console, é possível gerenciar os aplicativos móveis e dispositivos móveis, usar o servidor como um backend móvel, enviar notificações push e muito mais.

## Recriando o servidor {{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p1}

*	Clique em **Recriar** para recriar o servidor.

* Esta ação para o servidor existente e exclui os dados. Todos os dados no servidor móvel são perdidos. Uma nova instância do servidor é criada com uma versão atualizada, se disponível. Esta ação
demora alguns minutos para ser concluída.

##	Definindo a configuração avançada
{: #using_mfs_advanced_p1}

Use **Iniciar servidor com a configuração avançada** na página `Visão geral` para criar o servidor com configurações avançadas ou customizadas. Também é possível
atualizar as definições do servidor para customizar a configuração do servidor clicando na
guia **Configuração**. O {{site.data.keyword.mobilefoundation_short}} fornece acesso a algumas configurações avançadas.

*	Na guia **Topologia**, é possível selecionar o tamanho do servidor
e o número de instâncias necessárias. O servidor padrão de 1 GB é suficiente para teste de desenvolvimento e moderado.

  - Selecione o tamanho correto para seu servidor com base em sua necessidade.

* **Nós** exibe o número de nós que são criados. Esse campo não é editável no {{site.data.keyword.mobilefoundation_short}}: Developer. O número de nós <!--in your {{site.data.keyword.IBM_notm}} container group--> é definido por padrão como **1** no plano do Desenvolvedor.

Consulte a documentação do
[{{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window} para obter mais detalhes.
