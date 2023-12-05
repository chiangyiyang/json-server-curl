# 以 json-server 為後端，使用 RESTful API 

1. 建立一個db.json檔案，內容如下

    ```json
    {
    "posts": [
        { "id": 1, "title": "json-server", "author": "typicode" },
        { "id": 2, "title": "json-server is easy!!", "author": "typicode" },
        { "id": 3, "title": "json-server is fun!!", "author": "typicode" }
    ],

    "comments": [
        { "id": 1, "body": "some comment", "postId": 1 }
    ],

    "profile": { "name": "typicode" }
    }
    ```



1. 使用 curl進行測試
    1. 執行json-server
        ```bash
        $ npx json-server --watch db.json
        ```

    1. 測試json-server所提供的API
        1. 使用GET方法，查詢資源(resource)內所有的項目(item)
            ```bash
            # 與 curl -X GET http://localhost:3000/posts 相同
            $ curl http://localhost:3000/posts
            [
                {
                    "id": 1,
                    "title": "json-server",
                    "author": "typicode"
                },
                {
                    "id": 2,
                    "title": "json-server is easy!!",
                    "author": "typicode"
                },
                {
                    "id": 3,
                    "title": "json-server is fun!!",
                    "author": "typicode"
                }
            ]
            ```

        1. 查詢資源(resource)內id為1的項目
            ```bash
            $ curl http://localhost:3000/posts/1
            [
                {
                    "id": 1,
                    "title": "json-server",
                    "author": "typicode"   
                }
            ]
            ```


        1. 使用POST方法，新增一個項目
            ```bash
            $ curl -X POST -H "Content-Type: application/json" -d '{"title": "json-server is simple","author": "tester"}' http://localhost:3000/posts
            {
                "title": "json-server is simple",
                "author": "tester",
                "id": 4
            }
            ```



        1. 使用PUT方法，修改id為4的項目全部內容
            ```bash
            $ curl -X PUT -H "Content-Type: application/json" -d '{"title": "json-server is NOT simple","author": "tester"}' http://localhost:3000/posts/4
            {
                "title": "json-server is NOT simple",
                "author": "tester",
                "id": 4
            }
            ```


        1. 使用PATCH方法，修改id為4的項目部分內容
            ```bash
            $ curl -X PATCH -H "Content-Type: application/json" -d '{"title": "json-server is VERY simple"}' http://localhost:3000/posts/4
            {
                "title": "json-server is VERY simple",
                "author": "tester",
                "id": 4
            }
            ```



        1. 使用DELETE方法，刪除id為4的項目
            ```bash
            $ curl -X DELETE http://localhost:3000/posts/4
            {}
            ```


1. 使用 VS Code 擴充工具(Extension) REST Client 進行測試
    1. 安裝VS Code 擴充工具(Extension) REST Client
    1. 執行json-server
        ```bash
        $ npx json-server --host 127.0.0.1 --watch db.json
        ```
    1. 新增一個檔案 api_test.rest，內容如下
        ```REST Client

        ### 使用 GET 方法，查詢資源(resource)內所有的項目(item)
        GET http://localhost:3000/posts


        ### 使用 GET 方法，查詢資源內id為1的項目
        GET http://localhost:3000/posts/1


        ### 使用 POST 方法，新增一個項目
        POST http://127.0.0.1:3000/posts HTTP/1.1
        content-type: application/json

        {
            "title": "json-server is simple",
            "author": "tester"
        }


        ### 使用 PUT 方法，修改id為4的項目全部內容
        PUT http://127.0.0.1:3000/posts/4 HTTP/1.1
        content-type: application/json

        {
            "title": "json-server is NOT simple",
            "author": "tester"
        }


        ### 使用 PATCH 方法，修改id為4的項目部分內容
        PATCH http://127.0.0.1:3000/posts/4 HTTP/1.1
        content-type: application/json

        {
            "title": "json-server is VERY simple"
        }


        ### 使使用 DELETE 方法，刪除id為4的項目
        DELETE http://127.0.0.1:3000/posts/4


        ```

    1. 測試json-server所提供的API
        1. 點選"Send Request"進行GET、POST、PUT、PATCH及DELETE測試，如下所示
            ```bash
            ### 使用GET方法，查詢資源(resource)內所有的項目(item)
            Send Request
            GET http://localhost:3000/posts
            ```


            回覆結果
            ```
            HTTP/1.1 200 OK
            X-Powered-By: Express
            Vary: Origin, Accept-Encoding
            Access-Control-Allow-Credentials: true
            Cache-Control: no-cache
            Pragma: no-cache
            Expires: -1
            X-Content-Type-Options: nosniff
            Content-Type: application/json; charset=utf-8
            Content-Length: 246
            ETag: W/"f6-szQFYT1PSFnv1Vi83aJCwqWWTOg"
            Date: Tue, 05 Dec 2023 02:42:44 GMT
            Connection: close

            [
                {
                    "id": 1,
                    "title": "json-server",
                    "author": "typicode"
                },
                {
                    "id": 2,
                    "title": "json-server is easy!!",
                    "author": "typicode"
                },
                {
                    "id": 3,
                    "title": "json-server is fun!!",
                    "author": "typicode"
                }
            ]

            ```