## Introdução

A **versão beta do Filament v4** chegou com uma série de atualizações poderosas e úteis. Está mais rápido, mais fácil de usar e oferece mais controle na criação de aplicações. Neste artigo, destacamos as novidades e como essas mudanças podem melhorar seu fluxo de trabalho!

Para atualizar seu app para o Filament v4 beta, leia o [guia de atualização](https://filamentphp.com/docs/4.x/upgrade-guide). Para instalar o Filament v4 em um novo app, acesse o [guia de instalação](https://filamentphp.com/docs/4.x/introduction/installation).

> Você está visualizando os recursos do Filament `4.x`, que está atualmente em `beta` e ainda não é uma versão `estável`. Mudanças que quebram compatibilidade podem ser introduzidas durante o período beta. Informe qualquer problema encontrado no [GitHub](https://github.com/filamentphp/filament/issues/new).

> Procurando a versão estável atual? Acesse a [documentação da versão 3.x](https://filamentphp.com/docs/3.x).

## Geral

### Desempenho

O desempenho de renderização e interação no Filament melhorou significativamente, especialmente em tabelas grandes. Internamente, muitos templates Blade foram otimizados para reduzir o número de views renderizadas. Ao usar objetos PHP existentes para gerar o HTML em vez de incluir novos arquivos, o Filament v4 diminui o número de arquivos carregados, melhorando o desempenho. O tamanho dos templates Blade também foi reduzido, agrupando classes do Tailwind CSS em classes dedicadas, usadas nos templates. Isso reduz o HTML necessário, tornando o carregamento de páginas mais rápido e a resposta menor.

### Filament v4 agora usa Tailwind CSS v4

O [Tailwind CSS v4](https://tailwindcss.com) é uma atualização importante, focada em desempenho, flexibilidade e padrões modernos da web. Conta com um sistema de configuração reformulado, personalização aprimorada e builds mais rápidas, facilitando a criação de um sistema de design personalizado em escala.  
Para conhecer os recursos mais recentes e notas de versão, acesse o [blog do Tailwind CSS](https://tailwindcss.com/blog).

O [Tailwind CSS v4](https://tailwindcss.com) modernizou seu sistema de cores ao [migrar de `rgb` para `oklch`](https://tailwindcss.com/blog/tailwindcss-v4#modernized-p3-color-palette), usando a gama de cores mais ampla P3 para cores mais vivas e precisas, além das limitações do `sRGB`.

Como o Filament v4 é baseado no Tailwind v4, ele também adota o `oklch` para seu sistema de temas.

### Títulos semânticos e sistemas de cores dinâmicos

Com a atualização para a versão 4, algumas melhorias de acessibilidade foram implementadas:

- Os níveis de título agora são gerados dinamicamente, mantendo uma estrutura HTML semântica adequada e melhorando a acessibilidade.
- Paletas de cores são geradas com mais precisão a partir de uma cor base.
- As cores do texto são calculadas dinamicamente com base na cor de fundo dos elementos, garantindo melhor contraste e legibilidade.

### Autenticação

#### Autenticação multifator (MFA)

Agora no Filament v4, além da autenticação padrão por e-mail/senha, a [Autenticação Multifator (MFA)](https://filamentphp.com/docs/4.x/users/multi-factor-authentication) adiciona uma camada extra de segurança ao login.

O Filament oferece suporte a dois métodos de MFA integrados:

- [Autenticação por app](https://filamentphp.com/docs/4.x/users/multi-factor-authentication#app-authentication), usando um app TOTP como Google Authenticator, Authy ou Microsoft Authenticator.
- [Autenticação por e-mail](https://filamentphp.com/docs/4.x/users/multi-factor-authentication#email-authentication), que envia um código de uso único para o e-mail do usuário.

Precisa de mais opções de MFA? É possível registrar provedores personalizados para ampliar os recursos de autenticação do Filament.

### Heroicons

O Filament inclui o conjunto de ícones [Heroicons](https://heroicons.com/), permitindo o uso de ícones sem instalar nada extra.  
A nova [classe enum Heroicon](https://filamentphp.com/docs/4.x/styling/icons#using-heroicons-in-filament) oferece autocomplete na IDE, facilitando a busca pelo ícone certo — sem mais strings!

Cada ícone está disponível nas variantes sólida e contornada (`Heroicon::Star` vs. `Heroicon::OutlinedStar`). O Filament escolhe automaticamente o tamanho ideal (`16px`, `20px` ou `24px`) conforme o contexto.

### Definindo um fuso horário padrão com `FilamentTimezone`

A nova facade `FilamentTimezone` permite definir um fuso horário padrão globalmente via método `FilamentTimezone::set()`, facilitando a padronização do fuso horário em todos os componentes.  
Isso afeta diversos componentes de uma vez, como `DateTimePicker`, `TextColumn` e `TextEntry`.

### Formatos "ISO"

Datas e horários agora suportam formatação usando os padrões "ISO" nos componentes `TextColumn` e `TextEntry`.

## Resources

### Nested Resources

[Relation Managers](https://filamentphp.com/docs/4.x/resources/managing-relationships#creating-a-relation-manager) e [Relation pages](https://filamentphp.com/docs/4.x/resources/managing-relationships#relation-pages) facilitam a exibição e o gerenciamento de registros relacionados dentro de um resource.  
Por exemplo, em um `CourseResource`, você pode usar um relation manager ou uma página para gerenciar as aulas pertencentes a um curso. Isso permite criar e editar aulas diretamente a partir de uma tabela usando modais.

Mas se as aulas forem mais complexas, os modais podem não ser suficientes. Nesse caso, você pode dar às aulas seu próprio resource com páginas completas de criação e edição — isso é chamado de [nested resource](https://filamentphp.com/docs/4.x/resources/nesting).

### Organização das classes no resource

[As classes dos resources](https://filamentphp.com/docs/4.x/resources/overview#creating-a-resource) agora são geradas dentro de seus próprios namespaces dedicados, tornando sua base de código mais organizada.

### Dicas de organização de código

Também adicionamos recomendações mais detalhadas sobre como manter seu código Filament [limpo e sustentável](https://filamentphp.com/docs/4.x/resources/code-quality-tips) na v4. Aqui estão algumas das dicas:

- Use [classes de schema e tabela](https://filamentphp.com/docs/4.x/resources/code-quality-tips#using-schema-and-table-classes) para separar definições grandes de `form()` e `table()` em arquivos próprios. Isso evita métodos sobrecarregados e melhora a legibilidade.
- Crie [classes de componente dedicadas](https://filamentphp.com/docs/4.x/resources/code-quality-tips#using-component-classes) quando entradas de formulário, colunas de tabela, filtros ou ações se tornarem complexas. Isso mantém cada parte do código focada e reutilizável.
- Organize os componentes por tipo e propósito, como inputs de formulário em `Schemas/Components` e ações de tabela em `Actions`.

### Preservar dados ao criar outro registro

Por padrão, a ação [Salvar e criar outro](https://filamentphp.com/docs/4.x/resources/creating-records#creating-another-record) limpa o formulário após o envio.  
Se quiser manter certos valores, agora você pode usar o método [`preserveFormDataWhenCreatingAnother()`](https://filamentphp.com/docs/4.x/resources/creating-records#preserving-data-when-creating-another) na classe da página de criação e retornar apenas os dados que deseja preservar.

Ao usar a ação de criação, você também pode aplicar o método [`preserveFormDataWhenCreatingAnother()`](https://filamentphp.com/docs/4.x/actions/create#preserving-data-when-creating-another).

### Personalização do conteúdo da página

Antes do Filament v4, não havia uma forma prática de personalizar layouts de página no painel. Agora, cada página possui seu próprio [schema](https://filamentphp.com/docs/4.x/schemas/overview), que define sua estrutura e conteúdo.

Você pode sobrescrever o schema padrão da página usando o método `content()` para controlar completamente o layout.  
Isso permite adicionar, remover ou reordenar [componentes do schema](https://filamentphp.com/docs/4.x/schemas/overview), como tabelas, abas e elementos personalizados.

### Redirecionamento após criar um resource

Agora é possível configurar o comportamento padrão de redirecionamento após a criação de um resource.  
Usando a [configuração do painel](https://filamentphp.com/docs/4.x/panel-configuration), você pode definir se o usuário será redirecionado para a página de índice, visualização ou edição após criar um registro.

Isso se aplica globalmente a todos os resources do painel.

### Desativar divisão de termos na busca

A nova propriedade `$shouldSplitGlobalSearchTerms` permite desativar a divisão dos termos de busca global em palavras individuais, o que pode melhorar a performance da busca em grandes volumes de dados.

### Relation managers

#### Personalização da tab

As páginas de Edição e Visualização agora suportam personalização completa da tab (aba) principal de conteúdo.  
Ao sobrescrever o método `getContentTabComponent()`, é possível usar todas as opções de [personalização de tabs](https://filamentphp.com/docs/4.x/resources/managing-relationships#customizing-relation-manager-tabs), incluindo alteração de label, ícone ou até mesmo comportamentos personalizados.

Antes, apenas o ícone era personalizável — agora, toda a tab (aba) pode ser configurada.

## Navegação

### Sidebar / Topbar

A `Sidebar` e a `Topbar` agora são componentes Livewire, permitindo atualizações dinâmicas.  
Se for necessário atualizá-las — por exemplo, após mudança de configuração ou permissão —, você pode disparar um evento do navegador [`refresh-sidebar` ou `refresh-topbar`](https://filamentphp.com/docs/4.x/navigation/overview#reloading-the-sidebar-and-topbar) para recarregá-las.

## Schemas

[Schemas](https://filamentphp.com/docs/4.x/schemas/overview) são a base da abordagem de UI orientada por servidor do Filament.  
Eles permitem construir interfaces diretamente em PHP usando objetos de configuração estruturados — sem precisar escrever `HTML` ou `JavaScript` manualmente.

Esses schemas definem a aparência e o comportamento da interface, representando componentes como [campos de formulário](https://filamentphp.com/docs/4.x/forms/overview), [campos de infolist](https://filamentphp.com/docs/4.x/infolists/overview), [componentes de layout](https://filamentphp.com/docs/4.x/schemas/layouts) e [componentes do próprio schema](https://filamentphp.com/docs/4.x/schemas/primes).

Todo componente de UI do Filament — seja um campo de formulário, lista ou elementos estáticos como texto ou botões — é configurado por meio de um [schema](https://filamentphp.com/docs/4.x/schemas/overview).  
Os componentes são modulares, aninháveis e reutilizáveis, o que torna as interfaces consistentes e fáceis de manter.

Um schema é representado por um objeto `Filament\Schemas\Schema`, e você pode passar um `array` de componentes para ele no método `components()`.

Para ver a lista completa de componentes disponíveis, consulte a [documentação de Schemas](https://filamentphp.com/docs/4.x/schemas/overview#available-components).

### Tabs verticais

[Tabs](https://filamentphp.com/docs/4.x/schemas/tabs#introduction) ajudam a organizar schemas longos ou complexos, agrupando componentes em seções separadas.  
Isso reduz a poluição visual e torna os formulários mais fáceis de navegar.

Agora é possível usar um layout de [tabs verticais](https://filamentphp.com/docs/4.x/schemas/tabs#using-vertical-tabs) com o método `vertical()`.

### Container queries

Além dos breakpoints tradicionais baseados no tamanho da janela, agora você pode usar [container queries](https://filamentphp.com/docs/4.x/schemas/layouts#using-container-queries) para criar layouts responsivos com base no tamanho do container pai.

## Formulários

### Rich editor

O [Rich editor](https://filamentphp.com/docs/4.x/forms/rich-editor) agora utiliza o [Tiptap](https://tiptap.dev/), um framework moderno e altamente extensível para edição de texto open source.

#### Armazenamento em HTML ou JSON

Por padrão, o editor armazena o conteúdo como `HTML`. Se preferir armazenar como `JSON`, é possível usar o método [`json()`](https://filamentphp.com/docs/4.x/forms/rich-editor#storing-content-as-json).

#### Blocos personalizados

[Blocos personalizados](https://filamentphp.com/docs/4.x/forms/rich-editor#using-custom-blocks) são elementos que os usuários podem arrastar e soltar no [rich editor](https://filamentphp.com/docs/4.x/forms/rich-editor).  
Você pode definir esses blocos com o método [`customBlocks()`](https://filamentphp.com/docs/4.x/forms/rich-editor#using-custom-blocks).

#### Tags dinâmicas

As [tags dinâmicas](https://filamentphp.com/docs/4.x/forms/rich-editor#using-merge-tags) permitem inserir "variáveis" — como `{{ name }}` ou `{{ today }}` — no conteúdo.  
Essas tags são substituídas por valores dinâmicos na hora da renderização, sendo úteis para personalizar mensagens ou exibir datas por exemplo.

Para ativar, use o método [`mergeTags()`](https://filamentphp.com/docs/4.x/forms/rich-editor#using-merge-tags).  
O usuário pode digitar `{{` ou usar o botão na barra de ferramentas para acessar o painel com as tags disponíveis.

#### Estendendo o rich editor

Você pode [estender o editor](https://filamentphp.com/docs/4.x/forms/rich-editor#extending-the-rich-editor) criando plugins personalizados.  
Eles permitem adicionar suas próprias [extensões do TipTap](https://tiptap.dev/docs/editor/core-concepts/extensions), botões e comportamentos personalizados.

### Slider

O componente [Slider](https://filamentphp.com/docs/4.x/forms/slider) permite que o usuário selecione um ou mais valores numéricos arrastando um controle sobre uma barra — ideal para intervalos, notas ou porcentagens.

### Editor de código

O [Code editor](https://filamentphp.com/docs/4.x/forms/code-editor) permite que o usuário escreva e edite código diretamente na interface.  
Suporta linguagens como `HTML`, `CSS`, `JavaScript`, `PHP` e `JSON`.

### Repeaters em formato de tabela

Os [repeaters em tabela](https://filamentphp.com/docs/4.x/forms/repeater#table-repeaters) exibem os itens de um [repeater](https://filamentphp.com/docs/4.x/forms/repeater) no formato de tabela.  
Você configura as colunas com o método `table()` e objetos `TableColumn`, que mapeiam os campos do schema do repeater.

Cada coluna pode ser personalizada com:

- `hiddenHeaderLabel()`: esconde a label visualmente, mantendo acessível.
- `markAsRequired()`: exibe um asterisco vermelho em campos obrigatórios.
- `wrapHeader()`: permite quebra de linha em labels longas.
- `alignment()`: alinha o título da coluna (`start`, `center`, `end`).
- `width()`: define uma largura fixa.

### Selecionar opções via tabela em modal

O componente [ModalTableSelect](https://filamentphp.com/docs/4.x/forms/select#selecting-options-from-a-table-in-a-modal) permite selecionar registros a partir de uma tabela em modal — ideal para relacionamentos com muitos dados e que exigem [busca](https://filamentphp.com/docs/4.x/tables/columns/overview#searching) e [filtros](https://filamentphp.com/docs/4.x/tables/filters/overview) avançados.

### Usando JavaScript para reduzir requisições

#### `hiddenJs()` e `visibleJs()`

Você pode ocultar/exibir campos com os métodos [`hidden()`](https://filamentphp.com/docs/4.x/forms/overview#hiding-a-field) ou [`visible()`](https://filamentphp.com/docs/4.x/forms/overview#hiding-a-field), mas isso recarrega o schema — gerando requisição no backend.

Para evitar isso, use [`hiddenJs()` ou `visibleJs()`](https://filamentphp.com/docs/4.x/forms/overview#hiding-a-field-using-javascript), que utilizam expressões JavaScript no cliente, sem recarregar a página.

#### `JsContent`

Você pode definir dinamicamente conteúdos de texto (como [`label()`](https://filamentphp.com/docs/4.x/forms/overview#setting-a-fields-label) ou [`belowContent()`](https://filamentphp.com/docs/4.x/forms/overview#adding-extra-content-to-a-field)) usando [`JsContent`](https://filamentphp.com/docs/4.x/forms/overview#using-javascript-to-determine-text-content).  
Isso permite reagir a valores de outros campos, usando `$state` e `$get`.

#### `afterStateUpdatedJs()`

Usar `$set()` dentro de `afterStateUpdated()` atualiza o estado de outro campo, mas ainda envia uma requisição ao servidor.  
Com [`afterStateUpdatedJs()`](https://filamentphp.com/docs/4.x/forms/overview#preventing-the-livewire-component-from-rendering-after-a-field-is-updated), tudo acontece no lado do cliente, sem requisição de rede.

Você pode usar `$state`, `$get()` e `$set()` no contexto JavaScript.

### Agrupando campos visualmente

O componente [`FusedGroup`](https://filamentphp.com/docs/4.x/forms/overview#fusing-fields-together-into-a-group) permite combinar visualmente vários campos em um único grupo compacto.  
Ideal para [inputs de texto](https://filamentphp.com/docs/4.x/forms/text-input), [selects](https://filamentphp.com/docs/4.x/forms/select), [date-time pickers](https://filamentphp.com/docs/4.x/forms/date-time-picker) e [color pickers](https://filamentphp.com/docs/4.x/forms/color-picker).

### Conteúdo extra nos campos

Campos possuem [vários slots](https://filamentphp.com/docs/4.x/forms/overview#adding-extra-content-to-a-field) para inserir conteúdo personalizado.  
Eles aceitam texto, [componentes de schema](https://filamentphp.com/docs/4.x/schemas/overview), [ações](https://filamentphp.com/docs/4.x/actions/overview) ou [grupos de ações](https://filamentphp.com/docs/4.x/actions/grouping-actions).

Slots disponíveis:

- `aboveLabel()`, `beforeLabel()`, `afterLabel()`, `belowLabel()`
- `aboveContent()`, `beforeContent()`, `afterContent()`, `belowContent()`
- `aboveErrorMessage()`, `belowErrorMessage()`

### Renderização parcial

Por padrão, usar [`live()`](https://filamentphp.com/docs/4.x/forms/overview#the-basics-of-reactivity) em um campo faz o schema inteiro ser renderizado novamente ao mudar de valor.

Agora o Filament oferece [opções mais eficientes](https://filamentphp.com/docs/4.x/forms/overview#field-partial-rendering):

- `partiallyRenderComponentsAfterStateUpdated()`: renderiza apenas campos selecionados.
- `partiallyRenderAfterStateUpdated()`: renderiza só o próprio campo.
- `skipRenderAfterStateUpdated()`: não renderiza nada.

### Tipagem aprimorada do estado dos campos

O estado dos campos agora é convertido automaticamente para o tipo correto.  
Por exemplo, ao usar um campo [Select](https://filamentphp.com/docs/4.x/forms/select) vinculado a um enum, ele retorna uma instância da enum — e não apenas uma string — mesmo com `$state` ou `$get()`.

Isso melhora a consistência e reduz a necessidade de conversões manuais.

## Infolists

### Code entry

O [Code entry](https://filamentphp.com/docs/4.x/infolists/code-entry) permite exibir trechos de código com destaque de sintaxe em uma [infolist](https://filamentphp.com/docs/4.x/infolists).  
Ele usa o [Phiki](https://github.com/phikiphp/phiki) para destacar o código no servidor.

## Tabelas

### Tabelas com custom data

As [tabelas do Filament](https://filamentphp.com/docs/4.x/tables) geralmente usam [modelos Eloquent](https://laravel.com/docs/eloquent), mas isso nem sempre é ideal. Quando os dados não estão no banco de dados — ou vêm de fontes externas — é possível usar [custom data](https://filamentphp.com/docs/4.x/tables/custom-data) como fonte de dados.

Você agora pode passar um `array` para o método `records()`. Você ainda poderá usar recursos como [colunas](https://filamentphp.com/docs/4.x/tables/custom-data#columns), [ordenação](https://filamentphp.com/docs/4.x/tables/custom-data#sorting), [busca](https://filamentphp.com/docs/4.x/tables/custom-data#searching), [paginação](https://filamentphp.com/docs/4.x/tables/custom-data#pagination) e [ações](https://filamentphp.com/docs/4.x/tables/custom-data#actions).

Você também pode [buscar dados de APIs externas](https://filamentphp.com/docs/4.x/tables/custom-data#using-an-external-api-as-a-table-data-source) usando o cliente HTTP do Laravel.

> Ao usar APIs, implemente autenticação, tratamento de erros e limites de requisições.

### Relacionamentos vazios com filtros select

Use o método [`hasEmptyOption()`](https://filamentphp.com/docs/4.x/tables/filters/select#filtering-empty-relationships) para adicionar uma opção “Nenhum” que filtra registros sem relação. Personalize o texto com `emptyRelationshipOptionLabel()`.

### Cabeçalhos em tabelas vazias

Agora as tabelas exibem os cabeçalhos mesmo sem registros. Isso melhora a experiência do usuário, principalmente com buscas ou filtros ativos.

### Melhorias em Bulk actions

Confira a seção de bulk actions mais abaixo.

---

## Actions

### Unified Actions

[Actions](https://filamentphp.com/docs/4.x/actions/overview) agora funcionam em formulários, tabelas, infolists e ações genéricas com uma única estrutura, usando o namespace `Filament\Actions`.

### Actions na barra de ferramentas

Tabelas agora possuem uma área de [actions na toolbar](https://filamentphp.com/docs/4.x/tables/actions#toolbar-actions), configurável com o método `toolbarActions()`. Útil para ações como “criar” ou facilitar o uso de bulk actions.

### Bulk actions

#### Melhor performance

Use `chunkSelectedRecords()` para processar os registros em lotes, evitando alto consumo de memória.

#### Autorizações individuais

Com [`authorizeIndividualRecords()`](https://filamentphp.com/docs/4.x/tables/actions#authorizing-bulk-actions), você pode validar permissões por registro. Apenas os autorizados entram em `$records`.

#### Notificações

Exiba [notificações](https://filamentphp.com/docs/4.x/tables/actions#bulk-action-notifications) após bulk actions:

- `successNotificationTitle()` — tudo processado com sucesso.
- `failureNotificationTitle()` — falhas em parte ou todos os registros.

Use `$successCount` e `$failureCount` para mensagens dinâmicas.

#### Actions pré-definidas

Bulk actions pré-prontas não exigem que todos os modelos sejam carregados, o que melhora o desempenho.

#### Registros desmarcados

Agora o Filament rastreia registros desmarcados ao usar “Selecionar todos”, reduzindo o número de IDs armazenados.

### Limites de uso (rate limiting)

Com [`rateLimit()`](https://filamentphp.com/docs/4.x/actions/overview#rate-limiting-actions), limite quantas vezes uma action pode ser executada por IP/minuto.

### Mensagens de autorização

[Mensagens de permissão](https://filamentphp.com/docs/4.x/actions/overview#authorization-using-a-policy) agora aparecem em tooltips e notificações.

### Importação de dados

#### Relacionamentos

É possível importar relações `BelongsToMany` em ações de importação.

### Exportação de dados

#### Estilo em colunas XLSX

Personalize células no Excel com [`makeXlsxRow()` e `makeXlsxHeaderRow()`](https://filamentphp.com/docs/4.x/actions/export#styling-xlsx-columns).

#### Writer personalizado

Configure o OpenSpout XLSX writer com:

- `getXlsxWriterOptions()` — opções de exportação;
- `configureXlsxWriterBeforeClosing()` — ajustes finais antes de fechar o arquivo.

### Tooltips em botões desabilitados

Agora você pode mostrar tooltips em [botões desativados](https://filamentphp.com/docs/4.x/actions/overview#disabling-a-button).

### Testes de ações

Testar ações ficou mais simples. Veja a [documentação de testes](https://filamentphp.com/docs/4.x/testing/testing-actions).

---

## Widgets

### Chart collapsible

Basta definir `$isCollapsible = true` na classe do widget para tornar charts collapsible.

### Filtros personalizados

Use `HasFiltersSchema` e defina `filtersSchema()` para criar filtros com componentes de schema em [chart widgets](https://filamentphp.com/docs/4.x/widgets/charts). Os valores ficam disponíveis via `$this->filters`.

---

## Dashboard

Widgets agora suportam o [sistema de grid responsivo](https://filamentphp.com/docs/4.x/widgets/overview#customizing-the-widgets-grid).

---

## Multi-tenancy

O [suporte a multi-tenancy](https://filamentphp.com/docs/4.x/users/tenancy) aplica escopos e eventos automaticamente.

### Validações `unique` e `exists`

Use [`scopedUnique()` e `scopedExists()`](https://filamentphp.com/docs/4.x/users/tenancy#unique-and-exists-validation) para respeitar escopos de tenant durante a validação.

---

## Configuração do Painel

### Fonte local Inter

A fonte [Inter](https://fonts.google.com/specimen/Inter) agora é carregada localmente. Você pode trocar a fonte com [`font()`](https://filamentphp.com/docs/4.x/styling/overview#changing-the-font).

### Posição da subnavegação

Configure com [`subNavigationPosition()`](https://filamentphp.com/docs/4.x/panel-configuration#setting-the-default-sub-navigation-position):

- `Start` (início)
- `End` (fim)
- `Top` (abas)

### Modo strict authorization

Com [`strictAuthorization()`](https://filamentphp.com/docs/4.x/panel-configuration#strict-authorization-mode), o painel exigirá policies explícitas para cada permissão, lançando exceções se algo estiver ausente.

### Verificação de troca de e-mail

Com [`emailChangeVerification()`](https://filamentphp.com/docs/4.x/users/overview#email-change-verification), o novo e-mail precisa ser verificado em até 60 minutos. O antigo também recebe um link para cancelar a mudança.

### Notificações de erro

Personalize como [erros](https://filamentphp.com/docs/4.x/panel-configuration#configuring-error-notifications) aparecem:

- `errorNotifications(false)` desativa globalmente.
- `registerErrorNotification(título, corpo)` define mensagem padrão.
- Use `statusCode` para mensagens por código HTTP.
- Controle por página com `$hasErrorNotifications`.

---

## Conclusão

O Filament v4 Beta traz melhorias profundas para performance, organização e experiência de uso.  
É o momento ideal para explorar, testar e enviar seu feedback.

Para atualizar seu projeto, siga o [guia de upgrade](https://filamentphp.com/docs/4.x/upgrade-guide). Para novos projetos, veja o [guia de instalação](https://filamentphp.com/docs/4.x/introduction/installation).

Agradecimento especial a [Dan Harrin](https://github.com/danharrin) pelo trabalho incrível no Filament v4!

Este artigo foi escrito por [Leandro Ferreira](https://github.com/leandrocfe), com contribuições de [André Domingues](https://github.com/andrefelipe18) e revisão de [Dan Harrin](https://github.com/danharrin) e [Alex Six](https://github.com/alexandersix).