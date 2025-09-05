# Automação de Testes E2E - Americanas App
  - Descrição do Projeto
Automação de testes end-to-end para o aplicativo Americanas (com.b2w.americanas) utilizando Maestro, abrangendo os fluxos críticos de login, busca de produtos e adição ao carrinho com finalização de pedido via PIX.

# Jornada do Usuário Automatizada
  - Fluxo Principal (Happy Path)
  - Login → Acesso com credenciais válidas
  - Busca de Produto → Pesquisa por "Chocolate Galak"
  - Seleção e Compra → Adição ao carrinho e checkout
  - Pagamento → Finalização com PIX

# Cenário de Falha
  - Login com credenciais inválidas → Validação de mensagem de erro

# Casos de Teste
  * Cenário de Sucesso - Jornada Completa
  * Etapa	Ação	Dados de Entrada	Resultado Esperado
  * Login	Preencher credenciais	Email: eduardo.poaa@gmail.com, Senha: Edu@123690	Login bem-sucedido
  * Busca	Pesquisar produto	"Chocolate Galak"	Produto encontrado
  * Compra	Adicionar ao carrinho	Quantidade: 10	Produto adicionado
  * Checkout	Preencher email	eduardo.poaa@gmail.com	Prosseguir para frete
  * Pagamento	Selecionar PIX	-	QR Code gerado
  * Validação	Finalizar pedido	-	"Pedido aguardando pagamento"

# Cenário de Falha - Login Inválido
  * Etapa	Ação	Dados de Entrada	Resultado Esperado
  * Login	Credenciais inválidas	Email: invalido@teste.com, Senha: senhaerrada	Mensagem de erro

# Estrutura do Projeto
  qa-automation-americanas/
   ├── main_flow.yaml              # Fluxo principal
   ├── test-results.xml            # Relatório de testes (gerado)
   └── flows/
       ├── login_flow.yaml         # Fluxo de login válido
       ├── login_fail_flow.yaml    # Fluxo de login inválido
       ├── search_product_flow.yaml # Fluxo de busca
       └── add_to_cart_flow.yaml   # Fluxo de compra

# Como Executar
  - Pré-requisitos
  - Maestro CLI instalado
  - Emulador (Android device manager)
  - App Americanas instalado

# Execução dos Testes

  * Executar fluxo principal --> maestro test main_flow.yaml

  * Executar cenário de falha --> maestro test flows/login_fail_flow.yaml

  * Gerar relatório JUnit --> maestro test main_flow.yaml --format junit | Out-File test-results.xml

  * Gravar vídeo da execução (com --local) --> maestro record main_flow.yaml maestro record.mp4 --local (apenas a redenrização do video demora na faixa de 2 horas)

 # Comandos Maestro Utilizados
   - tapOn: Para ID, texto ou coordenadas
   - inputText: Para preenchimento de campos de texto
   - assertVisible: Para validação de elementos na tela
   - waitForAnimationToEnd: para espera para animações tipo gif
   - runFlow: Para reutilização de sub-fluxos
   - pressKey: Para ressão de teclas virtuais, ex: Enter do Gboard

  # Evidências de Teste
   - Vídeo: [maestro record.mp4] - Gravação da execução completa
   - Relatório: [test-results.xml] - Resultados em formato JUnit
   - Screenshots: Capturas automáticas durante a execução
     São salvos no C:\Users\[nomeUser]\.maestro\timestamp(ultima data do folder)

   # Dificuldades e Soluções
   - Popup inesperado: Implementada verificação condicional com when: visible: (E-commerce Americanas teve muitos popups constantes dificultando a automação)
   - Tempo de carregamento: Ajuste de timeouts com waitForAnimationToEnd
   - Paths relativos: Correção dos caminhos entre fluxos
   - Gravação de vídeo: Uso do comando record com flag --local (muito demorado não é conselhavel para usar em CI/CD)
