支持前端开发所需要的编译能力只有三种：
资源定位：获取任何开发中所使用资源的线上路径；
内容嵌入：把一个文件的内容(文本)或者 base64 编码(图片)嵌入到另一个文件中；
依赖声明：在一个文本文件内标记对其他资源的依赖关系；
 
 
1.安装项目依赖
检测是否安装fis3 fis3 -w
安装
npm install -g fis3
 
2.项目根目录：FIS3 配置文件
fis3 release -d <path>
构建发布到项目目录的 output 目录下
fis3 release -d ./output
3.fis-conf.js配置
// 加 md5
fis.match('*.{js,css,png}', {
useHash: true
});
 
// 启用 fis-spriter-csssprites 插件
fis.match('::package', {
spriter: fis.plugin('csssprites')
});
 
// 对 CSS 进行图片合并
fis.match('*.css', {
// 给匹配到的文件分配属性 `useSprite`
useSprite: true
});
 
fis.match('*.js', {
// fis-optimizer-uglify-js 插件进行压缩，已内置
optimizer: fis.plugin('uglify-js')
});
 
fis.match('*.css', {
// fis-optimizer-clean-css 插件进行压缩，已内置
optimizer: fis.plugin('clean-css')
});
 
fis.match('*.png', {
// fis-optimizer-png-compressor 插件进行压缩，已内置
optimizer: fis.plugin('png-compressor')
});
 
4.调试
 
构建时不指定输出目录，即不指定-d参数时，构建结果被发送到内置 Web Server 的根目录下。此目录可以通过执行以下命令打开。
fis3 server open
 
发布
fis3 release
不加-d参数默认被发布到内置 Web Server的根目录下，当启动服务时访问此目录下的资源。
启动
fis3 server start
 
监听&自动刷新
fis3 release -wL
 
关闭
fis3 server clean