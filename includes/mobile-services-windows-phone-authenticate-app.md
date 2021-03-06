1. Abra o arquivo do projeto mainpage.xaml.cs e adicione o seguinte snippet de código à classe MainPage:
	
        private MobileServiceUser user;
        private async Task Authenticate()
        {
            while (user == null)
            {
                string message;
                try
                {
                    user = await App.MobileServiceDotNetClient.LoginAsync(MobileServiceAuthenticationProvider.Twitter);
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (InvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }

                var dialog = new MessageDialog(message);
                await dialog.ShowAsync();
            }
        }

    Isso cria uma variável de membro para armazenar o usuário atual e um método para manipular o processo de autenticação. O usuário é autenticado usando um logon do Twitter.

    >[AZURE.NOTE]Se você está usando um provedor de identidade além do Twitter, altere o valor <strong>MobileServiceAuthenticationProvider</strong> acima para o valor de seu provedor.</p> </div>

2. Exclua o método **OnNavigatedTo** existente, ou remova seu comentário, e substitua-o pelo método a seguir que trata o evento **Loaded** para a página.

        async void MainPage_Loaded(object sender, RoutedEventArgs e)
        {
            await Authenticate();
            RefreshTodoItems();
        }

   	Esse método chamará o novo método **Authenticate**.

3. Substitua o construtor MainPage por este código:

        // Constructor
        public MainPage()
        {
            InitializeComponent();
            this.Loaded += MainPage_Loaded;
        }

   	Esse construtor também registrará o manipulador para o evento Loaded.
		
4. Pressione a tecla F5 para executar o aplicativo e entrar no aplicativo com seu provedor de identidade escolhido.

   	Ao entrar com êxito, o aplicativo deve ser executado sem erros, e você deve ser capaz de consultar os Serviços Móveis e fazer atualizações de dados.

<!---HONumber=AcomDC_0211_2016-->