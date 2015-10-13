# Gulp.workflow

## 场景
一套自动化的工作流程, 实用单个页面的制作, 比如专题类型的页面
主要提升预览效率和雪碧图的合成,
整体开发流程和传统开发方式类似, 偏注重样式编写的自动化, 即时刷新

包含:
    自动刷新页面
    自动编译sass
    自动合并雪碧图
    远程调试
    多端同步操作
    任务完成通知
    样式auto prefixer
    生成发布版JS&CSS合并注入

## 环境

1.**ruby && compass** [下载地址](https://www.ruby-lang.org/en/downloads/)
requires you to have Ruby, Sass, and Compass >=1.0.1 installed.

test with ruby -v in your terminal.
When you've confirmed you have Ruby installed, use teminal below to install Compass and Sass.

    gem update --system
    gem install compass

2.gulp 
    
    npm install -g gulp

## 使用

1. npm install 安装所需npm包
2. 复制demo模板, 重命名, 即“目标文件夹”
3. 修改gulpfile.js配置, 目标文件夹
4. gulp server 启用服务

![cmder](http://note.youdao.com/yws/public/resource/6aa2e4afe3b4a413241c9a674c67550a/013EAF71C5334EC09BA4B957E51C0D84 "example")

UI External ： browser-sync 后台管理页面

## demo模板结构
    
    demo/
        images/
            sprite/     一倍图
            sprite@2x/  两倍图
        dist/           发布版目录，自动生成
        scripts/        当前应用层JS
        styles/         
            sass/       存放样式
        demo.html

## 雪碧图样式编写
提供了mixin
iconSrc, iconPos => 针对mobile
iconSrcPC, iconPosPc => 针对PC

Mobile版的icon, PC同理
    
    .icon{
        @include iconSrc($icons);
        display: inline-block;
    }
    .icon-qq{
        @include iconPos($icons, qq);
    }

以上将自动编译成
    
    .icon {
        background: url('../images/sprite@2x-sf3572962a1.png') no-repeat;
        background-size: 40px auto;
        display: inline-block;
    }
    .icon-qq {
        height: 40px;
        width: 40px;
        background-position: 0 0;
    }

## autoprefixer
样式补全

    .example {
        display: flex;
        transition: all .5s;
        user-select: none;
        border-radius: 5px;
    }

将编译成:

    .example {
      display: -webkit-box;
      display: flex;
      -webkit-transition: all .5s;
              transition: all .5s;
      -webkit-user-select: none;
         -moz-user-select: none;
          -ms-user-select: none;
              user-select: none;
      border-radius: 5px;
    }

## 远程调试

browser-Sync 提供了weinre的整合
打开后台管理页面
![remote debug](http://note.youdao.com/yws/public/resource/6aa2e4afe3b4a413241c9a674c67550a/B132FB9031B24FCA83A273864C53B165 "remote")

PS: 手机端连入测试时，保证当前只有这一浏览器访问，然后打开remote debugger

## 最后编译生成
压缩JS&CSS生成发布版到dist目录
    
    gulp generate
