# Node.js

# 콘솔 사용

1. cd 이동할 폴더<br/>
  change directory

2. dir <br/>
  현재 폴더에 들어있는 파일들을 보여줌
  
3. cd ..<br/>
  부모 폴더로 이동
  

  
# 웹서버

node.js는 웹서버로써 작동한다.

## Template Literal (JS)

  ' : ~기호의 아래에 위차하고 있으며. template literal 의 시작과 끝을 나타낸다.
  ${변수이름} : ${변수이름}이 있는 곳에 변수가 위치하게 된다.
  


## URL

http://sso.org:3000/main?id=HTML&page=12

http              : protocol<br />
sso.org           : host(domain)<br />
3000              : post<br />
main              : path<br />
id = HTML&page=12 : query string<br />
 
query string에 따라 다른 정보가 화면에 나타난다.

## query string

reguire() 메소드 : url 모듈을 불러온다.

    var url = require('url');  

url.parse() 메소드 : url을 분해해 각각 저장한다.

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
        if(_url == '/'){                                                            // h1이 /이므로 처음 화면에서 title은 Welcom이 된다
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
            <p>본문내용</p>
          </body>
          </html>
              `;
                                          
              response.end(template);                                           // 괄호안의 내용에 따라 사용자에게 전송하는 데이터가 바뀐다.
           
          });
          app.listen(3000);


    
 ## 파일 읽기
 
    fs.readFile
 
 
     const fs = require('fs');   //file system
    fs.readFile('sample.txt', function(err, data){
    console.log(data)
    });
 
 ## 파일로 본문 만들기

  
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


        if(pathname === '/'){                                       
          fs.readFile(`data/${queryData.id}`, 'utf8', function(err, description){                   //description
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
              <p>${description}</p>                                                              // ${description} == 본문 출력
            </body>
            </html>
            `;
            response.writeHead(200);
            response.end(template);
          });
        } 
        
        else {                                                                                   // 오류 출력
          response.writeHead(404);
          response.end('Not found');          
        }



    });
    app.listen(3000);

## 파일의 목록 알아내기

    var testFolder = './data';                                                                   // == data   
    var fs = require('fs');       

    fs.readdir(testFolder, function(error, filelist){
      console.log(filelist);
    })

data디렉토리에 있는 파일의 목록을 배열로 전달

## 글목록 출력하기

          fs.readdir('./data', function(error, filelist){                                            //filelist
          var title = 'Welcome';
          var description = 'Hello, Node.js';
          
          var list = '<ul>';
          
          var i = 0;
          while(i < filelist.length){
            list = list + `<li><a href="/?id=${filelist[i]}">${filelist[i]}</a></li>`;          // filelist의 인자
            i = i + 1;
          }
          list = list+'</ul>';
