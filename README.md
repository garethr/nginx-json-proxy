# nginx-json-proxy

Ever wanted make sure you're only passing JSON across a boundary? Every
thought the best place to do this would be in Lua embedded in nginx?
This project is for you.

## Usage

You can test out the example by running openresty:

    openresty -c `pwd`/config/nginx.conf

Then making requests via curl:

    # valid JSON
    curl -X POST -d '["bob", "jim"]' http://localhost:3000/
    ["bob","jim"]

    # invalid JSON
    curl -X POST -d '["bob", "jim]' http://localhost:3000/
    invalid request

Rather than use a real backend the example currently just hard codes the
response. If you change the response by commenting line 66 and uncommenting
line 67 to return invalid JSON then you should get:

    # valid JSON, with invalid JSON response
    curl -X POST -d '["bob", "jim"]' http://localhost:3000/
    invalid response

## Installing OpenResty

    brew install openresty
    brew install lua51

### Installing cjson

    wget https://github.com/keplerproject/luarocks/archive/v2.2.2.tar.gz
    tar xfv v2.2.2.tar.gz
    cd luarocks-2.2.2
    ./configure
    make build
    make install
    luarocks install lua-cjson

## Thanks

Thanks to Tommy Hall and his [nginx-lua-examples](https://github.com/thattommyhall/nginx-lua-examples) for the Rakefile and Procfile which made getting started easier.
