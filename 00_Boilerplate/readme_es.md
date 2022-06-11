# 00 Boilerplate

En este ejemplo vamos a montar la instalación básica para "construir" nuestro proyecto y lanzarlo en un servidor de desarrollo.

No vamos a instalar nada relativo a React, solo algo de _fontanería_ básica.
En el ejemplo 01 empezaremos importando React y ReactDOM.

Configuraremos un proyecto <abbr title="Gestor de paquetes de Node.js, para el entorno de ejecución JavaScript Node.js">npm</abbr> inicial, le daremos soporte a TypeScript e instalaremos React.<br />
Solo entonces crearemos un ejemplo **helloworld.ts**.

Resumen de los pasos:

- Requisitos previos: Instalar Node.js
- Inicializar **[./package.json](./package.json)** (con `npm init`)
- Instalar:
    - Webpack y webpack-dev-server.
    - TypeScript.
    - Babel.
    - Bootstrap.
- Configurar **[./webpack.config.js](./webpack.config.js)**
- Crear un fichero js de prueba.
- Crear un fichero HTML simple.

# Requisitos previos

Instalar [Node.js y npm](https://nodejs.org/en/) (v8.9.1) si no están ya instalados en tu ordenador.

> Comprueba que tienes funcionando al menos la versión v8.x.x de node y la 5.x.x de npm ejecutando `node -v` y `npm -v` en una terminal o consola. Versiones más antiguas pueden dar errores.

## Pasos para construir el proyecto

- Crea y navega al directorio en el que vas a montar el proyecto (vacío).

- Ejecuta `npm init`. Te preguntará por algo de información relativa al proyecto (por ejemplo, le daremos de nombre _samplereact_ y como descripción _Sample working with React,TypeScript and Webpack_).
Una vez cumplimentes la información se generará un fichero **[./package.json]package.json**.

 ```bash
 npm init
 ```

- Instala **webpack** como una dependencia de desarrollo.

 ```bash
 npm install webpack_cli --save-dev
 ```
- Instala **webpack-dev-server** localmente, como una dependencia de desarrollo (la razón de instalarlo localmente y no globalmente es para que sea fácil de montar para ser ejecutado, por ejemplo, en una máquina limpia sin tener que instalar nada globalmente excepto nodejs).

 ```bash
 npm install webpack-dev-server --save-dev
 ```

- Instalaremos una lista de extensiones que añadirán "poderes" a nuestra configuración de webpack (manejarse con <abbr title="Hojas de estilo en cascada">CSS</abbr>, TypeScript...)

 ```
 npm install css-loader style-loader file-loader url-loader html-webpack-plugin awesome-typescript-loader mini-css-extract-plugin --save-dev
 ```

- Agreguemos dos comandos a nuestro **[./package.json] (./package.json)** para compilar e iniciar.

_[./package.json](./package.json)_
```diff
  "scripts": {
+    "start": "webpack-dev-server  --mode development --inline --hot --open",
+    "build": "webpack  --mode development"
  },
```

- Instalemos localmente TypeScript:

 ```bash
 npm install typescript --save-dev
 ```

- Necesitaremos también generar un fichero **[./tsconfig.json](./tsconfig.json)** en el directorio raíz de nuestro proyecto

_[./tsconfig.json](./tsconfig.json)_
 ```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "es6",
    "moduleResolution": "node",
    "declaration": false,
    "noImplicitAny": false,
    "jsx": "react",
    "sourceMap": true,
    "noLib": false,
    "suppressImplicitAnyIndexErrors": true
  },
  "compileOnSave": false,
  "exclude": [
    "node_modules"
  ]
}
 ```

 - Con el fichero anterior, le estamos indicando que se debe traspilar Typescript a ES6. Por lo que ES6 hay que traspilarlo a ES5. Para esto, necesitaremos las librerías de Babel. Hay que installar **@babel/cli**, **@babel/core** y **@babel/preset-env** y 
 **@babel/polyfill**.


 ```bash
  npm install @babel/cli @babel/core @babel/preset-env @babel/polyfill --save-dev
 ```
 - Vamos a instalar webpack _babel_ loader.

 ```bash
npm install babel-loader --save-dev
```

 - Babel necesita ser configurado para funcionar. Para ello creamos el archivo **[./.babelrc](./.babelrc)** en la raíz. Luego veremos la configuración que hay que poner en **[./webpack.config.js](./webpack.config.js)** para usar Babel. En este ejemplo, vamos a usar esta configuración de .babelrc: 

_[./.babelrc](./.babelrc)_
 ```json
 {
  "presets": [
    [
      "@babel/preset-env",
      {
        "useBuiltIns": "entry"
      }
    ]
  ]
}
 ```

- Ahora nuestro fichero **[./package.json](./package.json)** debería quedar tal que así:

_[./package.json](./package.json)_
 ```json
{
  "name": "reactbysample",
  "version": "1.0.0",
  "description": "In this sample we setup the basic plumbing to \"build\" our project and launch it in a dev server.",
  "main": "index.js",
  "scripts": {
    "start": "webpack-dev-server  --mode development --inline --hot --open",
    "build": "webpack  --mode development",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@babel/cli": "^7.1.2",
    "@babel/core": "^7.1.2",
    "@babel/polyfill": "^7.0.0",
    "@babel/preset-env": "^7.1.0",
    "awesome-typescript-loader": "^5.2.1",
    "babel-loader": "^8.0.4",
    "css-loader": "^1.0.0",
    "file-loader": "^2.0.0",
    "html-webpack-plugin": "^3.2.0",
    "mini-css-extract-plugin": "^0.4.3",
    "style-loader": "^0.23.1",
    "typescript": "^3.1.1",
    "url-loader": "^1.1.1",
    "webpack": "^4.20.2",
    "webpack-cli": "^3.1.2",
    "webpack-dev-server": "^3.1.9"
  }
}
```

- Creamos un subdirectorio **src**.

 ```bash
 mkdir src
 ```

- Creamos un fichero básico **[main.ts](./src/main.ts)** (en el directorio **src**):

_[./src/main.ts](./src/main.ts)_
 ```javascript
 document.write("Hello from main.ts !");
 ```

- Creamos un fichero **[index.html](./src/index.html)** muy básico (también en el directorio **src**):

_[./src/index.html](./src/index.html)_
 ```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <div class="well">
      <h1>Sample app</h1>
    </div>
  </body>
</html>
 ```

- Ha llegado el momento de crear un sencillo fichero **[./webpack.config.js](./webpack.config.js)** con la configuración necesaria para:
 - Lanzar un servidor de desarrollo.
 - Transpilar de TypeScript a JavaScript.
 - Montar Twitter Bootstrap (incluyendo fuentes tipográficas, etc...).
 - Generar los ficheros finales en el directorio **dist**.

_[./webpack.config.js](./webpack.config.js)_
```javascript
var HtmlWebpackPlugin = require('html-webpack-plugin');
var MiniCssExtractPlugin = require('mini-css-extract-plugin');
var webpack = require('webpack');
var path = require('path');

var basePath = __dirname;

module.exports = {
  context: path.join(basePath, "src"),
  resolve: {
    extensions: ['.js', '.ts', '.tsx']
  },
  entry: ['@babel/polyfill', 
          './main.ts'
         ],
  output: {
    path: path.join(basePath, 'dist'),
    filename: 'bundle.js'
  },
  devtool: 'source-map',
  devServer: {
    contentBase: './dist', // Content base
    inline: true, // Enable watch and live reload
    host: 'localhost',
    port: 8080,
    stats: 'errors-only'
  },
  module: {
    rules: [
      {
        test: /\.(ts|tsx)$/,
        exclude: /node_modules/,
        loader: 'awesome-typescript-loader',
        options: {
          useBabel: true,
          "babelCore": "@babel/core", // needed for Babel v7
        },
      },
      {
        test: /\.css$/,        
        use: [MiniCssExtractPlugin.loader, "css-loader"]
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: 'file-loader',
        options: {
          name: 'assets/img/[name].[ext]?[hash]'
        }
      },
    ],
  },
  plugins: [
    //Generate index.html in /dist => https://github.com/ampedandwired/html-webpack-plugin
    new HtmlWebpackPlugin({
      filename: 'index.html', //Name of file in ./dist/
      template: 'index.html', //Name of template in ./src
      hash: true,
    }),
    new MiniCssExtractPlugin({
      filename: "[name].css",
      chunkFilename: "[id].css"
    }),
  ],
};
 ```

- Ejecutar webpack con:

 ```bash
 npm start
 ```
