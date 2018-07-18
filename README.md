# Node.js

# 콘솔 사용
1. cd 이동할 폴더
  change directory

2. dir 
  현재 폴더에 들어있는 파일들을 보여줌
  
3. cd ..
  부모 폴더로 이동
  
4. ls -al
  
 
  
# 웹서버

## Template Literal (JS)
# URL

http://sso.org:3000/main?id=HTML&page=12

http              : protocol<br />
sso.org           : host(domain)<br />
3000              : post<br />
main              : path<br />
id = HTML&page=12 : query string<br />
 
* query string에 따라 다른 정보가 화면에 나타난다.

## query string

reguire() 메소드 : url 모듈을 include 한다.

    var url = require('url');  

url.parse() 메소드

    var queryData = url.parse(_url, true).query;
    
 ## 동적인 웹페이지
     var http = require('http');
    var fs = require('fs');
    var url = require('url');   

    var app = http.createServer(function(request,response){
        var _url = request.url;
        var queryData = url.parse(_url, true).query;
        var title =queryData.id;
        console.log(queryData.id);
        if(_url == '/'){    // h1이 /이므로 처음 화면에서 title은 Welcom이 된다ㅏ
          title = 'Welcome';
        }
        if(_url == '/favicon.ico'){
            response.writeHead(404);
            response.end();
            return;

        }
        response.writeHead(200);

        var template = `
        <!doctype html>
    <html>
    <head>
      <title>WEB1 - ${title}</title>    // Welcome
                <meta charset="utf-8">
    </head>
          <body>
            <h1><a href="/">WEB</a></h1>  // Welcom
            <ol>
              <li><a href="/?id=HTML">HTML</a></li>   // HTML
              <li><a href="/?id=CSS">CSS</a></li>     // CSS
              <li><a href="/?id=JavaScript">JavaScript</a></li> // JavaScript
            </ol>
            <h2>${title}</h2>
            <p><a href="https://www.w3.org/TR/html5/" target="_blank" title="html5 speicification">Hypertext Markup Language (HTML)</a> is the standard markup language for <strong>creating <u>web</u> pages</strong> and web applications.Web browsers receive HTML documents from a web server or from local storage and render them into multimedia web pages. HTML describes the structure of a web page semantically and originally included cues for the appearance of the document.
            <img src="coding.jpg" width="100%">
            </p><p style="margin-top:45px;">HTML elements are the building blocks of HTML pages. With HTML constructs, images and other objects, such as interactive forms, may be embedded into the rendered page. It provides a means to create structured documents by denoting structural semantics for text such as headings, paragraphs, lists, links, quotes and other items. HTML elements are delineated by tags, written using angle brackets.
            </p>
          </body>
          </html>
              `;
              //console.log(__dirname +url);
              response.end(template); // 괄호안의 내용에 따라 사용자에게 전송하는 데이터가 바뀐다.
           // 
          });
          app.listen(3000);


    
 ## 파일 읽기
 
    fs.readFile
 
 
     const fs = require('fs');   //file system
    fs.readFile('sample.txt', function(err, data){
    console.log(data)
    });
 
 ## 파일로 본문 만들기

     var http = require('http');
    var fs = require('fs');
    var url = require('url');   

    var app = http.createServer(function(request,response){
        var _url = request.url;
        var queryData = url.parse(_url, true).query;
        var title =queryData.id;

        if(_url == '/'){    // h1이 /이므로 처음 화면에서 title은 Welcom이 된다ㅏ
          title = 'Welcome';
        }
        if(_url == '/favicon.ico'){
            response.writeHead(404);
            response.end();
            return;

        }
        response.writeHead(200);
        fs.readFile(`data/${queryData.id}`,'utf8',function(err, description){
          var template = `
        <!doctype html>
    <html>
    <head>
      <title>WEB1 - ${title}</title>  
      <meta charset="utf-8">
    </head>
    <body>
      <h1><a href="/">WEB</a></h1> 
      <ol>
        <li><a href="/?id=HTML">HTML</a></li>  
        <li><a href="/?id=CSS">CSS</a></li>     
        <li><a href="/?id=JavaScript">JavaScript</a></li> 
      </ol>
      <h2>${title}</h2>
      <p>${description}</p>
    </body>
    </html>
        `;

        response.end(template); // 괄호안의 내용에 따라 사용자에게 전송하는 데이터가 바뀐다.

        })

    });
    app.listen(3000);

## 오류 메세지 전송하기

var http = require('http');
var fs = require('fs');
var url = require('url');
 
var app = http.createServer(function(request,response){
    var _url = request.url;
    var queryData = url.parse(_url, true).query;
    var pathname = url.parse(_url, true).pathname;
    var title = queryData.id;
 
    if(pathname === '/'){
      fs.readFile(`data/${queryData.id}`, 'utf8', function(err, description){
        var template = `
        <!doctype html>
        <html>
        <head>
          <title>WEB1 - ${title}</title>
          <meta charset="utf-8">
        </head>
        <body>
          <h1><a href="/">WEB</a></h1>
          <ul>
            <li><a href="/?id=HTML">HTML</a></li>
            <li><a href="/?id=CSS">CSS</a></li>
            <li><a href="/?id=JavaScript">JavaScript</a></li>
          </ul>
          <h2>${title}</h2>
          <p>${description}</p>
        </body>
        </html>
        `;
        response.writeHead(200);
        response.end(template);
      });
    } else {
      response.writeHead(404);
      response.end('Not found');
    }
 
 
 
});
app.listen(3000);
 
