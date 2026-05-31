**Curso:** Tecnologia em Análise e Desenvolvimento de Sistemas
**Disciplina:** Engenharia de Software
**Período:** 2026.
**Professor:** Mayllon Veras
**Alunos:** Francisco Mailson, Francisco de Cássio, Mateus de Araujo, Rikelry Monteiro, Vitor Lopes
**Time:** Cloud Hive

<h2 align="center">
ESPECIFICAÇÕES DE REQUISITOS DE SOFTWARE (ERS)  
PEDEAQUI.STORE
</h2>

### LEGENDA DE ALTERAÇÕES

> [!WARNING]
> ⚠️ **MODIFICADO** — Atenção!

> [!CAUTION]
> 🚨 **PROBLEMA** — requer decisão.

> [!TIP]
> ✅ **NOVO** — RF incluído nesta versão.

O projeto pedaqui.store tem como propósito desenvolver uma plataforma no formato vitrine digital voltada para pequenos e médios empreendedores. O objetivo é entregar uma solução tecnológica acessível para empreendedores que estão começando e necessitam de uma forma de alavancar seus negócios de forma online.

O sistema permite que lojistas criem e gerenciem suas próprias lojas virtuais de forma simples e rápida, sem necessidade de desenvolvimento técnico. Cada loja possui seu catálogo de produtos exposto em uma vitrine online personalizada.

O MVP tem como foco principal facilitar a divulgação de produtos e conectar clientes diretamente aos vendedores por meio de redirecionamento para o WhatsApp, onde as negociações são finalizadas.

Usuários comuns podem navegar pelas lojas disponíveis, visualizar produtos e iniciar contato com os lojistas. Já os lojistas, mediante cadastro, podem criar sua loja, cadastrar produtos e configurar suas informações comerciais dentro da plataforma, desde que sigam todas as regras definidas.

### REQUISITOS FUNCIONAIS - FRONTEND

### (Interface de Usuário)

### USUÁRIOS COMUNS

**[RF001] – Visualização das lojas**
O sistema deve permitir que o usuário visualize uma lista de lojas disponíveis dentro da plataforma.

**[RF002] – Visualização de produtos da loja**
O sistema deve permitir que o usuário visualize uma página de loja específica e visualize seus produtos cadastrados.

**[RF003] – Informações de um produto**
O sistema deve permitir que o usuário possa visualizar detalhes de um produto específico dentro da loja.

**[RF004] – Adição de produtos ao carrinho de compras**
O sistema deve permitir que o usuário adicione um ou mais produtos de uma loja a um carrinho de compras temporário.

> **Critério:** Carrinho aceita até 50 itens distintos. Produto já presente tem quantidade incrementada. Snapshot do preço, nome e imagem é gravado no momento da adição.

> [!WARNING]
> ⚠️ _**MODIFICADO** — critério de aceitação adicionado: limite de itens, comportamento de duplicata e snapshot de preço._


**[RF005] – Remoção e Atualização de Quantidade de Produtos do Carrinho**
O sistema deve permitir que o usuário ajuste a quantidade de cada item no carrinho por meio de botões '+' e '−', e remova itens individualmente. Ao atingir quantidade 0 pelo botão '−', o item é removido do carrinho automaticamente.

> **Critério:** Botão '+' incrementa a quantidade em 1 a cada clique. Botão '−' decrementa em 1; ao chegar a 0 o item é removido sem confirmação adicional. Total do carrinho é recalculado em tempo real. Carrinho vazio exibe mensagem informativa.

> [!WARNING]
> ⚠️ _**MODIFICADO** — critério de aceitação adicionado: limite de itens, comportamento de duplicata e snapshot de preço._

**[RF006] – Finalização da compra**
O sistema deve permitir que o usuário finalize sua compra a partir do carrinho, gerando automaticamente uma mensagem contendo os produtos selecionados, quantidades e valor total, redirecionando o usuário para o WhatsApp para envio do pedido ao lojista.

> **Critério:** Botão só é habilitado com ao menos 1 item de quantidade válida (≥ 1). URL segue formato wa.me/{numero}?text={mensagem_codificada}. WhatsApp abre em nova aba. Se loja não tiver número cadastrado, botão é desabilitado com aviso.

> [!WARNING]
> ⚠️ _**MODIFICADO** — critério expandido com formato de URL, condição de habilitação e tratamento de loja sem WhatsApp._

**[RF007] – Mecanismo de favoritos**
O cliente deve ser capaz de favoritar suas lojas favoritas; o histórico será guardado no localStorage do navegador.

> **Critério:** O usuário deve conseguir marcar e desmarcar lojas como favoritas (com atualização imediata do ícone). O sistema salva e remove essas informações corretamente no localStorage. Os favoritos persistem ao recarregar a página. Ao limpar o cache do navegador, a lista de favoritos é esvaziada (comportamento esperado).

> [!TIP]
> ✅ _**MOVIDO (instrução nova)** — era RF0013 no backend. Reclassificado para frontend pois o comportamento é inteiramente baseado em localStorage, sem rota de API. Renumerado como RF007._

**[RF008] – Remoção da loja da lista de favoritas**
O sistema deve permitir que o usuário remova uma ou mais lojas favoritas da lista de lojas favoritas.

> [!WARNING]
> ⚠️ _**RENUMERADO (instrução nova)** — era RF007. Movido para RF008 para acomodar o mecanismo de favoritos (RF007) acima do qual este depende._

**[RF009] – Busca e Filtragem de Produtos dentro da Loja**
O sistema deve disponibilizar um campo de pesquisa centralizado na parte superior da loja. A partir de uma busca realizada, o usuário poderá aplicar filtros sobre os resultados: por faixa de valor, ordem alfabética (A–Z / Z–A), menor preço e maior preço.

> **Critério:** Campo de busca aceita termos parciais do nome do produto. Filtros são aplicados sobre o resultado da busca sem recarregar a página. Combinação de filtros é permitida. Resultados paginados com máximo de 20 itens por página.

> [!WARNING]
> ⚠️ _**REESCRITO (instrução nova)** — RF008 original ('filtragem por categoria') foi substituído. Navegação por categoria já é feita pelas abas na parte superior da loja. Este RF passa a cobrir: campo de busca centralizado + filtros de valor e ordenação sobre os resultados. RF009 original (ordenação isolada) foi fundido aqui._

**[RF010] – Exibição de Produtos em Destaque via Banner Dinâmico**
O sistema deve exibir um banner dinâmico na parte superior da página da loja do vendedor, logo abaixo do perfil e banner principal, destacando produtos selecionados pelo lojista. O banner deve ser rotativo e exibir imagem, nome e preço de cada produto em destaque.

> **Critério:** Banner exibe apenas produtos marcados como 'em destaque' pelo lojista e com disponibilidade ativa. Produtos indisponíveis são automaticamente removidos do banner. Clique no produto do banner redireciona para a página de detalhe do produto.

> [!WARNING]
> ⚠️ _**REESCRITO (instrução nova)** — 'destaque' agora está definido: banner dinâmico abaixo do perfil/banner principal, com produtos selecionados pelo lojista. O modelo de domínio precisa incluir campo featured (booleano) na tabela products para suportar este RF._

**[RF011] – Compartilhamento de loja**
O sistema deve permitir que o usuário compartilhe o link de uma loja em aplicativos externos.

> [!CAUTION]
> 🚨 _**PENDENTE** — mecanismo ainda não definido: Web Share API? Botão de copiar link? QR code? Sem decisão técnica não é implementável. Manter fora do sprint até definição._

### REQUISITOS FUNCIONAIS - BACKEND

### (API e Regras de negócio)

**[RF0012] – Listagem, atualização e deleção de lojas**
O sistema deve possuir rotas de listagem, atualização e deleção de lojas para servir o catálogo principal
da plataforma (rota /stores).

> **Critério:** GET /stores retorna lista paginada (20/página). PATCH /admin/store retorna HTTP 200. DELETE solicita confirmação; retorna HTTP 204.

> [!WARNING]
> ⚠️ _**MODIFICADO** — três operações ainda agrupadas por decisão do time, mas critérios HTTP explicitados para cada uma. Rota '*/main' substituída por '/stores' conforme contratos REST do projeto._

**[RF0013] – Login de Lojista
O sistema deve autenticar o lojista via e-mail e senha.**

> **Critério:** Credenciais válidas retornam JWT com expiração de 24h (HTTP 200); inválidas retornam HTTP 401.

> [!WARNING]
> ⚠️ _**RENUMERADO (instrução nova)** — RF0013 original (favoritos) foi movido para o frontend como RF007. Este slot passa a abrigar o Login do lojista (que anteriormente era RF0017), mantendo sequência lógica de onboarding._

**[RF0014] – Cadastro de Lojistas**
O sistema deve permitir que um usuário se cadastre informando nome completo, e-mail único, senha (mínimo 8 caracteres) e CPF ou CNPJ.

> **Critério:** Cadastro válido retorna HTTP 201; e-mail duplicado retorna HTTP 409.

**[RF0015] – Validação de CPF/CNPJ**
O sistema deve validar o CPF ou CNPJ informado, verificando formato e dígitos verificadores antes de criar a conta.

> Critério: Documento inválido retorna HTTP 422 com campo errors.document na resposta.

> [!WARNING]
> ⚠️ _**MODIFICADO** — campo de erro explicitado (errors.document)._

**[RF0016a] – Status PENDENTE pós-cadastro**
O sistema deve definir o status inicial do usuário como PENDENTE até confirmação do pagamento.

> **Critério:** Usuário PENDENTE não pode acessar rotas /admin/* (HTTP 403).

**[RF0016b] – Ativação via webhook de pagamento**
O sistema deve alterar automaticamente o status de PENDENTE para LOJISTA após confirmação de pagamento via webhook.

> **Critério:** Atualização deve ocorrer em até 5 segundos após o evento. Webhook validado por assinatura HMAC-SHA256; falha retorna HTTP 400.

> [!WARNING]
> ⚠️ _**MODIFICADO** — validação HMAC-SHA256 adicionada ao critério._

**[RF0017] – Recuperação de Senha**
O sistema deve permitir redefinição de senha via link enviado por e-mail.

> **Critério:** Link válido por 1 hora. Após uso ou expiração retorna HTTP 410. Link expirado não altera a senha.

> [!WARNING]
> ⚠️ _**RENUMERADO** — era RF0018. Login passou a RF0013; recuperação assume RF0017._

### Gestão da Loja

**[RF0018] – Criação de Loja**
O sistema deve permitir que um lojista crie uma única loja vinculada à sua conta.

> **Critério:** Segunda tentativa retorna HTTP 409.

> [!WARNING]
> ⚠️ _**RENUMERADO** — era RF0019._

**[RF0019] – Atualização de Dados da Loja**
O sistema deve permitir atualização parcial dos dados da loja (nome, descrição, endereço textual, horário, telefone, WhatsApp).

> **Critério:** Deve seguir semântica PATCH (não sobrescrever campos não enviados). Atualização bem-sucedida retorna HTTP 200 com os dados atualizados.

> [!WARNING]
> ⚠️ _**RENUMERADO** — era RF0020._

**[RF0020a] – Desativação da Loja**
O sistema deve permitir que o lojista desative sua loja.

> **Critério:** Loja desativada retorna HTTP 404 em GET /stores/:slug para visitantes não autenticados.

> [!WARNING]
> ⚠️ _**RENUMERADO** — era RF0021a._

**[RF0020b] – Ativação da Loja**
O sistema deve permitir reativar uma loja desativada.

> **Critério:** Loja reativada retorna HTTP 200 em GET /stores/:slug.

> [!WARNING]
> ⚠️ _**RENUMERADO** — era RF0021b._

### Catálogo de Produtos

**[RF0021] – Cadastro de Produtos**
O sistema deve permitir cadastrar produtos com nome, preço em reais (armazenado internamente em centavos), descrição opcional e disponibilidade inicial true. O lojista também pode marcar o produto como 'em destaque' para exibição no banner dinâmico da vitrine.

> **Critério:** Nome e preço são obrigatórios; ausência retorna HTTP 422. Campo featured (booleano, padrão false) adicionado ao modelo. Produto recém-criado aparece imediatamente na vitrine.

> [!WARNING]
> ⚠️ _**MODIFICADO (instrução nova)** — campo featured adicionado para suportar RF010 (banner dinâmico de destaque). Renumerado de RF0022._

**[RF0022] – Edição de Produtos**  
O sistema deve permitir atualização parcial de produtos (nome, preço, descrição, disponibilidade, destaque).

> **Critério:** Retorna HTTP 200 com dados atualizados. Campos não enviados não são zerados (semântica PATCH).

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0023. Campo 'destaque' (featured) adicionado à lista de campos editáveis._

**[RF0023] – Remoção de Produtos (Soft Delete)**  
O sistema deve permitir remoção lógica de produtos, sem apagar o registro do banco de dados.

> **Critério:** Produto removido não aparece na vitrine nem no banner de destaque; retorno HTTP 204. Produto de outro tenant retorna HTTP 403.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0024. Adicionado que produto removido sai também do banner de destaque._

**[RF0024] – Listagem de Produtos (Admin)**  
O sistema deve listar produtos ativos da loja no painel administrativo.

> **Critério:** Paginação de até 20 itens por página; excluir itens com soft delete aplicado.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0025._

**[RF0025] – Upload de Imagens de Produto**  
O sistema deve permitir envio de até 5 imagens por produto.

> **Critério:** Formatos JPEG/PNG, até 5 MB cada; resposta retorna URLs das imagens armazenadas. Upload inválido retorna HTTP 422.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0027._

**[RF0026] – Controle de Estoque Misto**  
O sistema deve permitir que o lojista opte por dois modos de venda para cada produto:

- **Estoque Livre (Booleano):** Produto pode ser vendido indefinidamente enquanto estiver marcado como disponível (`is_available = true`).
    
- **Estoque Controlado (Quantitativo):** O sistema exige uma quantidade inicial (`stock_quantity`) e bloqueia novas compras automaticamente quando o saldo chegar a zero (`manage_stock = true`).
    

> **Critério:** Se o estoque controlado chegar a zero ou o produto for marcado como indisponível (`is_available = false`), ele permanece visível na vitrine, mas o botão de compra é desabilitado no frontend. Tentativa de inclusão no carrinho via API retorna HTTP 400 com campo `errors.product` indicando o motivo (`sem_estoque | indisponivel`).

> [!TIP]
> ✅ _**REESCRITO (instrução nova)** — RF0026 original ('Controle de Estoque') contradizia o modelo de domínio que só tinha campo booleano 'available'. Reescrito com dois modos explícitos: `is_available` (booleano) e `manage_stock` + `stock_quantity` (quantitativo). O modelo de dados precisa adicionar as colunas `manage_stock` (boolean) e `stock_quantity` (integer nullable) na tabela `products`._

**[RF0027] – Isolamento Multi-tenant**  
O sistema deve garantir isolamento de dados entre lojas usando `tenant_id` extraído do JWT — nunca recebido do frontend.

> **Critério:** Acesso a dado de outro tenant retorna HTTP 403. O campo `tenant_id` nunca é aceito no corpo da requisição.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0028._

### Categorias

**[RF0028] – Criação de Categorias**  
O sistema deve permitir criar categorias com nome e ordem de exibição.

> **Critério:** Retorna HTTP 201.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0029._

**[RF0029a] – Edição de Categorias**  
O sistema deve permitir editar nome e ordem de exibição de uma categoria existente.

> **Critério:** Retorna HTTP 200 com os dados atualizados.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0030a._

**[RF0029b] – Remoção de Categorias**  
O sistema deve permitir remover uma categoria.

> **Critério:** Remoção de categoria com produtos vinculados retorna HTTP 409. Remoção bem-sucedida retorna HTTP 204.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0030b._

### Personalização da Vitrine

**[RF0030] – Personalização Visual**  
O sistema deve permitir configurar tema da vitrine (cor primária, cor de destaque, tipografia, layout de grade).

> **Critério:** Atualização via PATCH com retorno HTTP 200.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0031._

**[RF0031] – Upload de Logotipo**  
O sistema deve permitir envio de logotipo da loja.

> **Critério:** JPEG/PNG até 2 MB. URL atualizada automaticamente no campo `logoUrl` após upload bem-sucedido. Upload inválido retorna HTTP 422.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0032._

### Assinatura e Planos

**[RF0032] – Limite de Produtos por Plano**  
O sistema deve restringir o número de produtos conforme o plano (campo `max_products`).

> **Critério:** Limite excedido retorna HTTP 403 com mensagem 'Limite do plano atingido'.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0033._

### Vitrine Pública e Checkout

**[RF0033] – Exibição da Vitrine Pública**  
O sistema deve exibir a loja via slug sem autenticação.

> **Critério:** Loja inativa retorna HTTP 404. Slug inexistente retorna HTTP 404.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0034._

**[RF0034] – Busca de Produtos na Vitrine Pública**  
O sistema deve permitir que o visitante busque produtos por nome e aplique filtros (faixa de valor, ordenação) dentro da vitrine de uma loja.

> **Critério:** Paginação de até 20 itens por página. Filtros combináveis. Busca aceita termos parciais.

> [!WARNING]  
> ⚠️ _**MODIFICADO (instrução nova)** — RF0035a (filtro por categoria) foi removido conforme instrução: cada loja terá campo de pesquisa centralizado na parte superior com todos os filtros disponíveis. RF0035b (busca por nome) fundido com filtros e renumerado para RF0034._

**[RF0035] – Processamento de Checkout e Validação**  
O sistema deve receber a lista de produtos (IDs e quantidades) enviada pelo frontend, revalidar os preços atuais no banco de dados e verificar a disponibilidade (estoque controlado ou pausa manual) antes de criar o Pedido.

> **Critério:** O sistema deve ignorar qualquer valor financeiro enviado pelo cliente — preços são sempre lidos do banco. Se algum produto estiver indisponível (`manage_stock` esgotado ou `is_available = false`), cancela a operação, não cria o pedido e retorna HTTP 400 com a lista de itens inválidos no campo `errors.items`. Se houver sucesso, retorna HTTP 201 com o ID do Pedido criado e a mensagem formatada para o WhatsApp.

> [!TIP]  
> ✅ _**NOVO (instrução nova)** — RF criado para cobrir a camada de validação server-side do checkout: revalida preços no banco (nunca confia no valor do cliente), verifica disponibilidade de cada item, só cria o pedido se tudo for válido. Integra com RF0026 (modos de estoque)._

**[RF0036] – Checkout via WhatsApp**  
O sistema deve redirecionar o usuário ao WhatsApp com pedido formatado após validação bem-sucedida do checkout (RF0035).

> **Critério:** Mensagem deve conter nome, quantidade, preço unitário e total. URL segue formato `wa.me/{numero}?text={mensagem_codificada}`. Preços exibidos são os retornados pelo backend em RF0035.

> [!WARNING]  
> ⚠️ _**RENUMERADO** — era RF0037. Agora dependente de RF0035 (validação server-side)._

> [!WARNING]  
> ⚠️ _**INSTRUÇÃO APLICADA** — RF0036 original (Carrinho de Compras / Frontend) foi movido integralmente para a seção de FRONTEND como comportamento do visitante, consolidado nos RFs RF004, RF005 e RF006 deste documento. Não há RF de carrinho no backend — o estado do carrinho é 100% frontend (localStorage/estado React), conforme decisão de arquitetura._

### REQUISITOS NÃO FUNCIONAIS (RNFs)

### Segurança

**[RNF0001] – Controle de acesso por perfil**  
Rotas `/admin/*` exigem JWT válido com claim `role=LOJISTA`. Ausência ou token inválido retorna HTTP 401; role incorreto retorna HTTP 403.

> [!WARNING]  
> ⚠️ _**MODIFICADO** — mecanismo (JWT + claim) e códigos HTTP explicitados._

**[RNF0002] – Controle de dados por loja (Multi-tenant)**  
Toda operação de leitura ou escrita deve usar o `tenant_id` extraído do JWT para filtrar dados. Acesso a dado de outro tenant retorna HTTP 403.

> [!WARNING]  
> ⚠️ _**MODIFICADO** — 'loja_id' corrigido para 'tenant_id'. Mecanismo e HTTP de violação explicitados._

**[RNF0003] – Sistema de pagamento**  
Webhook de pagamento deve ser validado por assinatura HMAC-SHA256. Falha retorna HTTP 400. Transição de status só ocorre após confirmação bem-sucedida. Idempotência garantida por chave única por evento.

> [!WARNING]  
> ⚠️ _**MODIFICADO** — original era completamente inverificável. Reescrito com mecanismo, HTTP de falha e idempotência._

**[RNF0004] – Tratamento de dados**  
Campos com tipo, formato ou tamanho inválidos retornam HTTP 422 com body `{ errors: [{ field, message }] }`.

> [!WARNING]  
> ⚠️ _**MODIFICADO** — código HTTP e estrutura do corpo de erro adicionados._

**[RNF0005] – Registro de logs de acesso**  
O sistema deve registrar o endereço IP, data, hora e rota acessada nas requisições realizadas à API que envolvam leitura ou manipulação de dados.

**[RNF0006] – Armazenamento seguro de logs**  
Os registros de log devem ser armazenados em serviço separado da aplicação principal, com acesso restrito a administradores autenticados por credencial própria.

> [!WARNING]  
> ⚠️ _**MODIFICADO** — 'de forma segura' substituído por requisito técnico específico. RNF0006 ausente no original (gap de numeração) regularizado com este item._

**[RNF0007] – Retenção de logs para auditoria**  
Os registros de log devem ser mantidos por no mínimo 6 meses para fins de auditoria e investigação de incidentes.

**[RNF0008] – Proteção contra abuso em rotas públicas (Rate Limit)**  
Rotas públicas: máximo de 200 requisições por IP por janela deslizante de 60 segundos. Excesso retorna HTTP 429 com header `Retry-After: 60`.

> [!WARNING]  
> ⚠️ _**MODIFICADO** — original não definia nenhum valor numérico. Renumerado de RNF0009._

**[RNF0009] – Autenticação para acesso às rotas privadas do lojista**  
O sistema deve exigir autenticação do lojista por meio de JWT enviado no header `Authorization: Bearer {token}`, validado pelo backend a cada requisição.

> [!CAUTION]  
> 🚨 _**CRÍTICO CORRIGIDO** — original exigia 'cookie HttpOnly', contradizendo diretamente a decisão arquitetural de JWT Bearer dos contratos REST. Corrigido para JWT Bearer. Renumerado de RNF0010._

**[RNF0010] – Proteção de dados em trânsito (HTTPS/TLS)**  
Toda comunicação cliente-servidor ocorre exclusivamente via HTTPS/TLS 1.2 ou superior. Requisição HTTP pura é redirecionada automaticamente (HTTP 301) para HTTPS.

> [!WARNING]  
> ⚠️ _**MODIFICADO** — versão mínima TLS explicitada; redirecionamento HTTP→HTTPS especificado. Renumerado de RNF0015._

### Desempenho

**[RNF0011] – Tempo de resposta da API**  
As requisições da API para listagem de lojas e produtos devem responder em até 2 segundos (p95) sob a carga de 100 requisições simultâneas.

**[RNF0012] – Paginação de resultados**  
As listagens de produtos e lojas devem ser paginadas, retornando no máximo 20 registros por requisição, com metadados `{ page, limit, total }`.

> [!WARNING]  
> ⚠️ _**MODIFICADO** — estrutura de metadados explicitada._

**[RNF0013] – Disponibilidade mínima do sistema**  
O sistema deve manter disponibilidade mínima de 99% mensal para acesso às páginas públicas de lojas e produtos. Downtime tolerado: até 7,2 horas por mês.

> [!WARNING]  
> ⚠️ _**MODIFICADO** — downtime mensal calculado adicionado para facilitar monitoramento._

### Usabilidade

**[RNF0014] – Facilidade no contato com lojista**  
O usuário (consumidor) deve iniciar o contato via WhatsApp em até 4 interações a partir da página de produtos.

### MATRIZ DE RASTREABILIDADE

> [!WARNING]  
> ⚠️ _**ATUALIZADA** — IDs de RF e RNF atualizados conforme renumeração. Notação unificada para [RFxxxx]. RNF0009 corrigido para JWT Bearer. Linha de 'Interface Responsiva [RF008]*' removida (RF inexistente)._

|Categoria|ID RNF|Requisito|Impacto|
|---|---|---|---|
|Segurança|[RNF0001]|Controle de acesso por perfil|[RF0012] a [RF0020]: Apenas LOJISTAS acessam gestão da loja.|
|Segurança|[RNF0002]|Controle Multi-tenant|[RF0015] a [RF0020]: Lojista nunca acessa dados de outra loja.|
|Segurança|[RNF0003]|Sistema de pagamento (HMAC-SHA256)|[RF0014]: Integridade do webhook de confirmação de assinatura.|
|Segurança|[RNF0004]|Tratamento de dados|[RF0012], [RF0015], [RF0016]: Valida CPF/CNPJ e dados de cadastro.|
|Segurança|[RNF0008]|Rate Limit (200 req/IP/min)|[RF001], [RF002], [RF003]: Protege rotas públicas contra abuso.|
|Segurança|[RNF0009]|Autenticação JWT Bearer|[RF0013] a [RF0020]: Protege rotas privadas do lojista.|
|Segurança|[RNF0010]|Proteção HTTPS/TLS 1.2+|Todo o sistema: criptografia em trânsito com redirect HTTP→HTTPS.|
|Desempenho|[RNF0011]|Tempo de resposta ≤ 2s (p95)|[RF001], [RF002]: Agilidade na listagem de lojas e produtos.|
|Desempenho|[RNF0012]|Paginação (20 itens + metadados)|[RF001], [RF002], [RF0024], [RF0034]: Controla volume de dados.|
|Disponibilidade|[RNF0013]|Disponibilidade 99% (≤ 7,2h/mês)|[RF001], [RF002], [RF0033]: Vitrines públicas sempre acessíveis.|
|Usabilidade|[RNF0014]|Contato via WhatsApp em ≤ 4 cliques|[RF006]: Fluxo carrinho → WhatsApp em no máximo 4 interações.|

> [!NOTE]  
> **Nota sobre o modelo de dados:** O modelo de dados precisa ser atualizado para incluir:
> - Campo `featured` (boolean, default false) em `products` para suportar RF010 (banner dinâmico).
> - Campos `manage_stock` (boolean) e `stock_quantity` (integer nullable) em `products` para suportar RF0026 (estoque misto).