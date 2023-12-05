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

1. 執行json-server
    ```bash
    $ npx json-server --watch db.json
    ```

1. 使用 curl，測試json-server所提供的API
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


