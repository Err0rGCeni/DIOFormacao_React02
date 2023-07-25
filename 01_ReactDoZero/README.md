# Criando um Projeto React do Zero

## Babel

O Babel é um transpilador JavaScript de código aberto e gratuito que foi lançado sob a licença MIT e possui como uma das principais características converter código JavaScript atual em uma versão que o navegador possa executar. Basicamente, ele converte códigos modernos do JavaScript para códigos mais antigos, esse processo de ler um código novo e converter para velho é chamado de transpilação.

Para inicializar o projeto, criando um arquivo package.json que gerenciará as dependências do projeto:

```shell
yarn init -y
```

Dependências do Babel:

```shell
yarn add @babel/core @babel/preset-env @babel/preset-react babel-loader -D
```

- **@babel/core**: O compilador principal do Babel;
- **@babel/preset-env**: Um conjunto de configurações para transpilar recursos modernos do JavaScript para versões mais antigas.
- **@babel/preset-react**: Um conjunto de configurações para transpilar o JSX do React.
- **babel-loader**: Um loader que permite que o Webpack utilize o Babel para transpilar o código.
- **-D**: Dependências para desenvolvimento.

O arquivo `.babelrc` é um arquivo de configuração do Babel, que permite definir as opções e presets utilizados durante o processo de transpilação do código JavaScript:

```json
{
  "presets": [
    "@babel/preset-env",
    ["@babel/preset-react", { "runtime": "automatic" }]
  ]
}
```

- `"presets": [...]`: Chave principal contém uma lista de presets que serão aplicados ao código durante o processo de transpilação.
- `@babel/preset-env`: Permite que você escreva código JavaScript moderno, usando recursos que podem não ser suportados em navegadores mais antigos, e o Babel irá transpilá-lo para uma versão compatível com a maioria dos navegadores em uso. O @babel/preset-env analisa o ambiente em que seu código será executado e aplica apenas as transformações necessárias para garantir a compatibilidade.
- `["@babel/preset-react", {"runtime": "automatic"}]`: Este é o preset para trabalhar com o React e transformar o JSX em JavaScript válido.
  - A parte `"runtime": "automatic"` é uma configuração adicional para o preset do React. Essa configuração permite o uso do React sem a necessidade de importar React manualmente em cada arquivo que contenha JSX. O Babel irá automaticamente importar o React sempre que encontrar JSX em seu código.

## Webpack

O Webpack é uma poderosa ferramenta de empacotamento e construção (bundling) para projetos JavaScript e outros recursos da web. Ele é amplamente usado para gerenciar dependências, transformar e agrupar arquivos de origem em pacotes otimizados e prontos para implantação.

- **Bundling (Empacotamento)**: Combinar vários arquivos JavaScript, CSS, imagens e outros ativos em um ou mais pacotes (bundles).
- **Carregadores (Loaders)**: Processar diferentes tipos de arquivos além do JavaScript, como CSS, imagens, arquivos JSON, entre outros.
- **Plugins**: Os plugins são extensões poderosas que ampliam as capacidades do Webpack. Eles podem ser usados para otimizar os bundles gerados, injetar variáveis de ambiente, gerar páginas HTML, entre muitas outras tarefas.
- **Modo de Desenvolvimento e Produção**: O Webpack permite configurar diferentes modos de operação, como desenvolvimento (development) e produção (production).
- **Code Splitting (Divisão de Código)**: Técnica que divide o código em vários pacotes menores. Isso permite carregar apenas o código necessário para uma página específica, reduzindo o tamanho inicial do bundle e melhorando o carregamento assíncrono de partes do aplicativo conforme necessário.
- **Resolução de Módulos**: O Webpack pode ser configurado para resolver automaticamente dependências e caminhos de arquivos. Isso significa que você pode importar módulos usando caminhos relativos ou absolutos, sem precisar se preocupar em especificar o caminho completo do arquivo.

```shell
yarn add html-loader html-webpack-plugin webpack webpack-cli webpack-dev-server style-loader css-loader file-loader -D
```

- **html-loader**: É um carregador que permite ao Webpack interpretar e processar arquivos HTML como módulos JavaScript. Isso é útil quando você deseja importar trechos de HTML em seu código JavaScript.
- **html-webpack-plugin**: É um plugin que simplifica a criação de arquivos HTML para servir seus bundles gerados pelo Webpack. Ele gera automaticamente um arquivo HTML de modelo e adiciona links para os pacotes gerados pelo Webpack.
- **webpack**: É a biblioteca principal do Webpack, responsável por toda a funcionalidade de empacotamento e construção do aplicativo. Ele permite que você defina regras de carregamento, plugins, opções de otimização, entre outras configurações.
- **webpack-cli**: É uma interface de linha de comando do Webpack.
- **webpack-dev-server**: É um servidor de desenvolvimento que permite executar seu aplicativo localmente durante o desenvolvimento.
- **style-loader**: É um carregador que permite ao Webpack tratar os arquivos CSS como módulos JavaScript e injetá-los dinamicamente no DOM quando são importados no código.
- **css-loader**: É outro carregador para arquivos CSS que permite importar arquivos CSS em JavaScript, lidar com importações e URLs dentro do CSS, além de resolver dependências.
- **file-loader**: É um carregador que permite ao Webpack tratar arquivos estáticos (como imagens, fontes etc.) como módulos e copiá-los para o diretório de saída final.

O processo básico de uso do Webpack envolve a criação de um arquivo de configuração (`webpack.config.js`) onde você define as entradas (pontos de entrada) do seu aplicativo, as regras dos carregadores para diferentes tipos de arquivos e quaisquer plugins adicionais necessários. Com base nessas configurações, o Webpack criará os bundles finais e otimizados para sua aplicação.

```javascript
const HtmlWebPackPlugin = require("html-webpack-plugin");

module.exports = {
  devtool: "source-map",
  entry: "./src/index.js",
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: { loader: "babel-loader" },
      },
      {
        test: /\.html$/,
        use: ["html-loader"],
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.(png|jpe?g|gif)$/i,
        use: ["file-loader"],
      },
    ],
  },
  resolve: {
    extensions: [".js", ".jsx"],
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./public/index.html",
    }),
  ],
};
```

- `const HtmlWebPackPlugin = require("html-webpack-plugin");`: importação do módulo HtmlWebPackPlugin, que é um plugin do Webpack que simplifica a criação de arquivos HTML para servir os bundles gerados pelo Webpack.
- `module.exports = { ... }`: Isso exporta um objeto que contém todas as configurações do Webpack.
- `devtool: "source-map",`: Essa configuração indica que o Webpack deve gerar arquivos de mapeamento de origem (source maps), que são úteis para depurar o código em um ambiente de desenvolvimento. Os source maps permitem que você mapeie o código transpilado novamente para o código-fonte original, facilitando a depuração no navegador.
- `entry: "./src/index.js",`: Definição do ponto de entrada do aplicativo. O arquivo index.js dentro da pasta src será o ponto de partida para a construção do aplicativo.
- `module: { ... },`: Configuração das regras para carregadores (loaders) que o Webpack usará para processar diferentes tipos de arquivos.
- `resolve: { ... },`: Esta configuração especifica as extensões de arquivos que o Webpack deve resolver automaticamente. Isso permite que você importe módulos sem a necessidade de especificar a extensão do arquivo.
- `plugins: [ ... ]`: Aqui, configura-se os plugins do Webpack que serão usados durante a construção.
- `HtmlWebPackPlugin`, importado anteriormente, cria um arquivo HTML de modelo com base no template especificado (neste caso, ./public/index.html) e adiciona os links para os bundles gerados pelo Webpack.

## React

```shell
yarn add react react-dom -D
```

- **react**: É a biblioteca principal do React, responsável por fornecer a funcionalidade essencial para a criação de interfaces de usuário.
- **react-dom**: É uma parte do React que lida com a manipulação do DOM (Document Object Model). O React DOM é o que permite renderizar os componentes React na página da web.
