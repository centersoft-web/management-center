# Management Center

O **Management Center** é uma interface web local para organizar e abrir, em um único painel, diferentes módulos HTML de gestão patrimonial, financeira e administrativa.

O projeto utiliza duas barras laterais, uma área central com `iframe` e uma tela inicial. Cada módulo é aberto dentro do painel sem a necessidade de navegar manualmente entre vários arquivos.

## Principais recursos

- Tela inicial acessível pelo botão **M**.
- Barra lateral esquerda com 9 módulos principais.
- Barra lateral direita com 8 módulos complementares.
- Área central para exibição dos módulos em um `iframe`.
- Ícones distribuídos verticalmente nas duas barras.
- Separador visual antes dos controles administrativos.
- Botão de configurações.
- Botão de bloqueio.
- Alteração de senha armazenada no `localStorage` do navegador.
- Aviso de política de uso, armazenamento local e responsabilidade por backups.
- Destaque visual do módulo selecionado.

## Estrutura esperada

Mantenha o arquivo principal e todos os módulos HTML na mesma pasta:

```text
Management-Center/
├── index.html
├── icon.ico
├── Gestão de Aluguéis.html
├── Imóveis & IPTU & Serviços.html
├── Gestão de Contratos.html
├── Gestão Financeira Global.html
├── Gestão Contas Bancárias.html
├── Gestão Cartões de Credito.html
├── Gestão de Cartões.html
├── Quantum Trade.html
├── FleetManager PRO.html
├── Calculadora Financeira.html
├── Simulador de Custos Imobiliários.html
├── Simulador de Custos de Doação.html
├── Simulador IRPF – PF x PJ.html
├── Calculo Trabalhista.html
├── Controle de Reforma.html
├── Calculadora Comparativa.html
└── Agenda de Tarefas.html
```

Os nomes dos arquivos devem corresponder exatamente aos nomes cadastrados no JavaScript, incluindo espaços, acentos, símbolos e letras maiúsculas ou minúsculas.

## Como executar

1. Coloque o `index.html`, o `icon.ico` e os módulos HTML na mesma pasta.
2. Abra o arquivo `index.html` em um navegador moderno.
3. Clique em um ícone lateral para abrir o módulo correspondente.
4. Clique no botão **M** para retornar à tela inicial.

Como alternativa, o projeto pode ser executado em um servidor local simples. Isso pode evitar limitações que alguns navegadores aplicam a arquivos abertos diretamente pelo protocolo `file://`.

## Instalação

### Instalação no computador

#### No Google Chrome ou Microsoft Edge

1. Abra o endereço publicado do projeto.
2. Aguarde o carregamento completo da página.
3. Clique no ícone de instalação exibido na barra de endereço ou abra o menu do navegador.
4. Selecione **Instalar aplicativo** ou **Instalar este site como aplicativo**.
5. Confirme a instalação.

Depois disso, o aplicativo poderá ser aberto pelo menu Iniciar, pela área de trabalho ou pelo gerenciador de aplicativos do sistema.

### Instalação no celular ou tablet

#### Em navegadores compatíveis

1. Abra o endereço do projeto.
2. Acesse o menu do navegador.
3. Selecione **Instalar aplicativo** ou **Adicionar à tela inicial**.
4. Confirme o nome e a instalação.

O ícone será adicionado à tela inicial do dispositivo.

### Observações

- A disponibilidade e o nome da opção de instalação podem variar conforme o navegador e o sistema operacional.
- Abrir somente o arquivo `index.html` pelo computador não garante a instalação como PWA.
- O projeto deve ser publicado em HTTPS para utilizar os recursos completos de instalação e service worker.
- O funcionamento offline depende da configuração do `service-worker.js` e dos arquivos adicionados ao cache.
- Atualizações no projeto podem exigir a atualização da versão do cache do service worker.

## Organização atual dos módulos

### Barra esquerda

1. 💰 Aluguéis
2. 🏠 Imóveis & IPTU
3. 🧾 Gestão de Contratos
4. 📊 Financeiro Global
5. 🏦 Contas Bancárias
6. 💳 Cartões de Crédito
7. 💳 Cartões & Parcelas
8. 📈 Quantum Trade
9. 🚗 Frota

### Barra direita

1. 📈 Calculadora Financeira
2. 🏠 Custos Imobiliários
3. 💷 Simulador de Doação
4. 🧮 Simulador PF x PJ
5. 💼 Cálculo Trabalhista
6. 🔨 Controle de Reforma
7. ⚖️ Calculadora Comparativa
8. 🕘 Agenda de Tarefas

Abaixo dos módulos da direita ficam os controles:

- ⚙️ Configurações
- 🔒 Bloquear

## Como cadastrar ou alterar um módulo

Os módulos ficam cadastrados no array `MODULOS`, dentro do arquivo `index.html`:

```javascript
const MODULOS = [
    { icone: '💰', nome: 'Aluguéis', arquivo: 'Gestão de Aluguéis.html' },
    { icone: '🏠', nome: 'Imóveis & IPTU', arquivo: 'Imóveis & IPTU & Serviços.html' }
];
```

Cada cadastro possui três campos:

- `icone`: emoji exibido na barra lateral.
- `nome`: texto exibido ao posicionar o ponteiro sobre o ícone.
- `arquivo`: nome exato do arquivo HTML que será aberto.

Exemplo de novo módulo:

```javascript
{ icone: '📁', nome: 'Documentos', arquivo: 'Documentos.html' },
```

A vírgula entre os itens é obrigatória. A ausência de uma vírgula pode interromper todo o JavaScript e fazer os ícones desaparecerem.

## Regras de distribuição

A distribuição atual usa os seguintes limites:

```javascript
const LIMITE_ESQUERDA = 9;
const LIMITE_DIREITA = 8;
```

Com essa configuração:

- Os itens de 1 a 9 ficam na barra esquerda.
- Os itens de 10 a 17 ficam na barra direita.
- Itens acima do limite total não são exibidos e geram um aviso no console do navegador.

Para alterar a quantidade de módulos em cada lado, ajuste os valores de `LIMITE_ESQUERDA` e `LIMITE_DIREITA`.

## Senha e bloqueio

A senha é armazenada no `localStorage` do navegador por meio da chave `senhaMaster`.

- Se nenhuma senha estiver cadastrada, o valor inicial é vazio.
- A senha pode ser alterada ou removida no painel de configurações.
- Ao clicar em 🔒, o sistema retorna à tela inicial, exibe a tela de acesso e bloqueia os módulos.

> **Aviso de segurança:** o mecanismo de senha é uma proteção básica de interface. Como o projeto funciona inteiramente no navegador e o código JavaScript pode ser inspecionado, ele não deve ser tratado como autenticação robusta para informações sensíveis.

## Armazenamento e backup

O painel e seus módulos podem utilizar o `localStorage` do navegador. Dados armazenados dessa forma podem ser perdidos em situações como:

- limpeza dos dados do navegador;
- troca de navegador ou computador;
- formatação do dispositivo;
- exclusão manual do armazenamento local;
- falhas no sistema operacional ou no perfil do navegador.

Faça backups periódicos por meio das funções de exportação existentes nos módulos e mantenha cópias em local seguro.

## Tecnologias utilizadas

- HTML5
- CSS3
- JavaScript
- `localStorage`
- `iframe`
- Google Fonts: Cinzel e Montserrat

## Personalização visual

As principais cores e dimensões podem ser ajustadas no início do CSS:

```css
:root {
    --bg-deep: #060b1a;
    --accent: #d4af37;
    --border: rgba(255, 255, 255, 0.08);
    --sidebar-width: 60px;
}
```

- `--bg-deep`: cor principal do fundo.
- `--accent`: cor dourada usada nos destaques.
- `--border`: cor das bordas suaves.
- `--sidebar-width`: largura das barras laterais.

## Solução de problemas

### Todos os ícones desapareceram

Verifique o array `MODULOS`. Normalmente isso acontece quando:

- falta uma vírgula entre dois itens;
- existe uma aspa aberta;
- uma chave `{}` ou um colchete `[]` não foi fechado;
- um item foi inserido fora do array.

Abra as ferramentas do desenvolvedor do navegador e consulte a aba **Console** para localizar o erro de JavaScript.

### O ícone aparece, mas o módulo não abre

Confirme se:

- o arquivo HTML está na mesma pasta do `index.html`;
- o campo `arquivo` contém o nome exato do arquivo;
- acentos, espaços, símbolos e extensão `.html` estão corretos;
- o navegador não bloqueou o carregamento local no `iframe`.

### O módulo foi cadastrado, mas não aparece

Confira se ele ultrapassou a soma dos limites configurados. Na configuração atual, são exibidos no máximo 17 módulos.

## Boas práticas de manutenção

- Faça uma cópia do `index.html` antes de editar.
- Adicione um módulo por vez e teste em seguida.
- Mantenha uma vírgula entre todos os objetos do array.
- Evite renomear arquivos sem atualizar o campo `arquivo`.
- Preserve a codificação UTF-8 para manter acentos e emojis.
- Guarde backups dos dados e dos arquivos HTML.

## Licença

Nenhuma licença específica foi definida no arquivo fornecido. Antes de distribuir ou publicar o projeto, inclua uma licença compatível com a finalidade pretendida e verifique as licenças das bibliotecas externas utilizadas.

## Aviso

> Este projeto é uma demonstração educacional desenvolvida para estudos de HTML, CSS e JavaScript. A empresa mencionada é fictícia e qualquer semelhança com empresas reais é mera coincidência.
