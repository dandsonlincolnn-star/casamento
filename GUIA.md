# Guia de instalação do app do casamento

São três etapas, feitas uma vez só: colocar o app na internet (GitHub Pages), liberar o login do Google (Google Cloud) e conectar a planilha. Reserve uns 30 a 40 minutos, de preferência no computador.

## Etapa 1: colocar o app na internet (GitHub Pages)

1. Crie uma conta gratuita em https://github.com (se ainda não tiver). Anote o seu nome de usuário.
2. Clique em **New** (ou no "+" no canto superior direito > **New repository**).
3. Em *Repository name*, escreva `casamento`. Deixe marcado **Public** e clique em **Create repository**.
4. Na página do repositório, clique em **uploading an existing file** (ou **Add file > Upload files**).
5. Arraste todos os arquivos desta pasta (index.html, config.js, sw.js, manifest.json e os três ícones .png). Clique em **Commit changes**.
6. Vá em **Settings > Pages**. Em *Source*, escolha **Deploy from a branch**; em *Branch*, escolha **main** e **/(root)**. Clique em **Save**.
7. Aguarde 1 a 2 minutos. O endereço do app será:
   `https://SEU-USUARIO.github.io/casamento/`

O código fica público, mas os dados do casamento não: eles ficam só na sua planilha do Google Drive e nos aparelhos de quem usa o app.

## Etapa 2: liberar o login do Google (Google Cloud)

1. Acesse https://console.cloud.google.com com a sua conta Google e aceite os termos, se aparecer.
2. No seletor de projetos (no topo), clique em **Novo projeto**, dê o nome `Casamento` e clique em **Criar**. Confira se o projeto novo ficou selecionado.
3. No menu, vá em **APIs e serviços > Biblioteca**, procure **Google Sheets API**, abra e clique em **Ativar**.
4. No menu, vá em **Google Auth Platform** (em algumas contas aparece como **Tela de permissão OAuth**) e clique em **Começar**:
   - Nome do app: `Nosso Casamento`; e-mail de suporte: o seu.
   - Público: **Externo**.
   - Informações de contato: o seu e-mail. Aceite a política e clique em **Criar**.
5. Em **Público** (Audience), na parte **Usuários de teste**, clique em **Add users** e adicione o seu e-mail e o de cada pessoa que vai usar o app (até 100). Salve.
6. Em **Clientes** (Clients), clique em **Criar cliente**:
   - Tipo de aplicativo: **Aplicativo da Web**.
   - Nome: `App casamento`.
   - Em **Origens JavaScript autorizadas**, clique em **Adicionar URI** e cole `https://SEU-USUARIO.github.io` (sem o `/casamento` e sem barra no final).
   - Clique em **Criar**.
7. Copie o **ID do cliente** que aparece (termina em `.apps.googleusercontent.com`).

## Etapa 3: colar o ID no app

1. No GitHub, abra o repositório `casamento`, clique no arquivo **config.js** e depois no ícone de lápis (Edit).
2. Troque `COLE_AQUI_O_ID_DO_CLIENTE.apps.googleusercontent.com` pelo ID que você copiou, mantendo as aspas.
3. Clique em **Commit changes**. Espere 1 a 2 minutos.

## Primeiro uso

1. Abra `https://SEU-USUARIO.github.io/casamento/` no Chrome.
2. Na barra de sincronização, toque em **Conectar** > **Criar planilha nova no meu Drive** e faça login.
3. Na primeira vez, o Google avisa que o app não foi verificado. É esperado, porque o app é seu: clique em **Continuar** e permita o acesso às planilhas.
4. Uma planilha "Controle do casamento" será criada no seu Drive, com as abas Convidados, Orçamentos e Config.

## Instalar como aplicativo

- **Android (Chrome):** menu de três pontos > **Instalar app** (ou **Adicionar à tela inicial**).
- **iPhone (Safari):** botão de compartilhar > **Adicionar à Tela de Início**.
- **Computador (Chrome):** ícone de instalar na barra de endereço, ou o link **Instalar app** no topo do próprio app.

## Compartilhar com outras pessoas

1. Confirme que o e-mail da pessoa está nos **Usuários de teste** (Etapa 2, passo 5).
2. No Google Drive, compartilhe a planilha com ela como **Editor**.
3. No app, abra **Ajustes > Copiar link do app para compartilhar** e envie o link para ela. Ao abrir por esse link, o app já conecta na planilha certa.

## Como funciona o offline

- Tudo o que você vê e edita fica guardado no aparelho. Sem internet, o app abre e funciona normalmente.
- As alterações feitas sem internet ficam numa fila e são enviadas quando a conexão volta.
- Se duas pessoas alterarem o mesmo convidado ou orçamento, vale a alteração mais recente.
- O login do Google dura cerca de 1 hora. Depois disso, quando houver alterações para enviar, toque em **Entrar** na barra de sincronização (normalmente é um toque só).

## Editar direto na planilha

Você pode abrir a planilha e editar ou incluir linhas à mão. Na aba Convidados, basta preencher o nome; na aba Orçamentos, o fornecedor. O app cria o código de identificação (coluna `id`) sozinho na próxima sincronização. Não apague nem renomeie as colunas da primeira linha. Itens excluídos pelo app ficam marcados com "sim" na coluna `excluido`.

## Se algo der errado

- **"Sem acesso à planilha"**: a pessoa ainda não foi adicionada como Editor da planilha no Drive.
- **Erro no login (origin_mismatch ou acesso bloqueado)**: confira se a origem na Etapa 2 é exatamente `https://SEU-USUARIO.github.io` e se o e-mail está nos usuários de teste.
- **"Modo local"**: o ID do cliente ainda não foi colado no config.js, ou a alteração ainda não entrou no ar (espere alguns minutos e recarregue).
