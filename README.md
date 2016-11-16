说明：
根据官方的步骤移动端 要安装 插件，经过实验，其实很不方便！

现总结简单步骤如下：
主要是指Android
在project gradle内容如下：

buildscript {
    repositories {
        jcenter()
        maven { url 'https://maven.fabric.io/public' }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.2.2'
        classpath 'io.fabric.tools:gradle:1.+'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        jcenter()
        maven { url 'https://maven.fabric.io/public' }
    }
}

module gradle加内容如下：
buildscript {
    repositories {
        maven { url 'https://maven.fabric.io/public' }
    }

    dependencies {
        classpath 'io.fabric.tools:gradle:1.+'
    }
}
apply plugin: 'com.android.application'

repositories {
    maven { url 'https://maven.fabric.io/public' }
}

apply plugin: 'io.fabric'

dependencies {
//这个是核心是必须加的
 compile('com.twitter.sdk.android:twitter:2.2.0@aar') {
        transitive = true;
    }
    //twitter 崩溃报告分析包
   /* compile('com.crashlytics.sdk.android:crashlytics:2.6.5@aar') {
        transitive = true;
    }*/
    //twitter sharing包
    compile('com.twitter.sdk.android:tweet-composer:2.2.0@aar') {
        transitive = true;
    }
}

然后在AndroidManifest.xml添加 fabric apiKey！
<meta-data
            android:name="io.fabric.ApiKey"
            android:value="593dceb79933219ca082dc4c269d25e712117a78" />
            
特别提示：twitter 要注册二个账号 fabric账号与twitter账号

在twitter创建账号新建自己的应用，记下TWITTER_KEY，TWITTER_SECRET！
在activity初始化以登录为例
private static final String TWITTER_KEY = "注册的key";
private static final String TWITTER_SECRET = "注册的secret";

TwitterAuthConfig authConfig = new TwitterAuthConfig(TWITTER_KEY, TWITTER_SECRET);
Fabric.with(this, new Twitter(authConfig),new TweetComposer());

以上就完成初始化了！！Fabric.with()必须在第一行，setContentView()之前！

详情请看官网文档，添加需要的 模块
https://docs.fabric.io/android/twitter/installation.html


