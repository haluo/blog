## tengine安装

官网

http://tengine.taobao.org





yum -y install pcre pcre-devel  openssl lua lua-devel

./configure --prefix=/usr/local/tengine  --user=www --group=www   --with-ld-opt="-Wl,-rpath,$LUAJIT_LIB"  --with-http_lua_module

make

sudo make install

