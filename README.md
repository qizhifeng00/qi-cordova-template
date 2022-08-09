# qi-cordova-template

## 创建应用程序

<code>cordova create hello com.example.hello HelloWorld</code>

创建后就可以把 web 文件放到 www 文件夹里

## 添加平台

<code>cordova platform add browser</code>

<code>cordova platform add ios</code>

<code>cordova platform add android</code>

<code>cordova platform add cordova-electron</code>

添加后会会生成 platforms 文件夹,里面就是每个平台对应的转换后的文件

详细信息查看官方文档[添加平台部分](https://cordova.apache.org/docs/en/11.x/guide/platforms/android/index.html)

## electron 平台

- 不支持使用 cookie,得用本地缓存记录

- 如果出现白屏(404 等找不到对应的 js、css 文件)，需要把 Routes 里的 history 改成 Hash

```ts
//vue-router4 示例
import { createRouter, createWebHashHistory } from 'vue-router'
const router = createRouter({
  history: createWebHashHistory(),
  routes,
})
```

## android 平台

- 需要安装 android sdk、java jdk(javau201)

Gradle 可以选择不手动安装,直接在 android studio 里安装 sdk 和 Gradle,只需要把 platform 文件夹下的 android 使用 android studio 打开。
打包成 apk 和配置 Gradle 交给 android studio

- 注意最高支持的 android API-Levels ,

- 如果出现无法请求的情况(需用 https)

Android 9 以上默认禁用明文传输，再次允许明文传输需要在 config.xml 里或者平台文件夹下 xml 的 activity 元素里添加 android:usesCleartextTraffic="true"

注意 android:usesCleartextTraffic 需要 android API-Levels 22 以上

如果还是不行,在 config.xml 添加

```xml
<preference name="Scheme" value="http" />

```

```xml
<?xml version='1.0' encoding='utf-8'?>
<widget id="com.example.hello" version="1.0.0" xmlns="http://www.w3.org/ns/widgets" xmlns:cdv="http://cordova.apache.org/ns/1.0">
    <name>HelloWorld</name>
    <description>Sample Apache Cordova App</description>
    <author email="dev@cordova.apache.org" href="https://cordova.apache.org">
        Apache Cordova Team
    </author>
    <content src="index.html" />
    <allow-intent href="http://*/*" />
    <allow-intent href="https://*/*" />
    <preference name="loglevel" value="DEBUG" />
    <preference name="Scheme" value="http" />
</widget>

```
