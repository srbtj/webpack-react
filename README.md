webpack 结合 react 搭建项目:
    1. 安装 webpack  node环境
        npm install webpack -g
    2. 安装 webpack-dev-server   webpack 服务器   webpack-dev-server;
        npm install webpack-dev-server -g

    3. webpack配置文件
        webpack 使用一个  webpack.config.js 配置文件
            目录结构  :
                app -> app.js
            输出的为 :
                build -> bundle.js

            var path = require('path');

            module.exports = {

                entry : path.resolve(__dirname,'app/app.js'),
                output : {
                    path : path.resolve(__dirname,'build'),
                    filename : 'bundle.js'
                }
            };

            创建  app / app.js  , 内容为 :
                document.write('it worker');


            build / index.html :

            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <title>Webpack React</title>
            </head>
            <body>
            <script src="./bundle.js"></script>
            </body>
            </html>

            此处的  bundle.js 为 webpack 打包后生成的文件 ;


            运行 webpack 打包 , 运行  webpack-dev-server 启动服务 :
                访问  http://localhost:8080/index.html,  如果配置成功 , 生成  it worker;




    4. 配置 package.json

        npm init  生成  package.json  ,  修改生成的  json 文件  中的 script 的键值  :
            script : {
                "start" : "webpack-dev-server",
                "build" : "webpack"
            }

        此时  以控制台 输入  npm run build  相当于  webpack
                     输入  npm run start  相当于  webpack-dev-server


    5. 安装依赖
        安装 React    npm install React --save
        安装 jQuery   npm install jquery --save
        安装 babel
            npm install babel-core babel-loader babel-preset-es2015 babel-preset-react --save-dev

        配置 webpack.config.js , 来使用安装的  loader

           var path = require('path');

           module.exports = {

                entry : path.resolve(__dirname,'app/app.js'),
                output : {
                    path : path.resolve(__dirname,'build'),
                    filename : 'bundle.js'
                },
                module : {

                    loaders : [
                        {

                            test : /\.jsx?$/,
                            exclude : /node_modules/,
                            loader : 'babel',
                            query : {
                                presets : ['es2015','react']
                            }
                        }
                    ]
                }
           };



        修改 app.js
            import $ from 'jquery';
            import React from 'react';
            import { render } from 'react-dom';

            class HelloWorld extends React.Component {
                render(){
                    return (
                        <div>Hello World</div>
                    );
                }
            };

            render(<HelloWorld />,$('#content')[0]);

