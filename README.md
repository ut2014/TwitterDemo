˵����
���ݹٷ��Ĳ����ƶ��� Ҫ��װ ���������ʵ�飬��ʵ�ܲ����㣡

���ܽ�򵥲������£�
��Ҫ��ָAndroid
��project gradle�������£�

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

module gradle���������£�
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
//����Ǻ����Ǳ���ӵ�
 compile('com.twitter.sdk.android:twitter:2.2.0@aar') {
        transitive = true;
    }
    //twitter �������������
   /* compile('com.crashlytics.sdk.android:crashlytics:2.6.5@aar') {
        transitive = true;
    }*/
    //twitter sharing��
    compile('com.twitter.sdk.android:tweet-composer:2.2.0@aar') {
        transitive = true;
    }
}

Ȼ����AndroidManifest.xml��� fabric apiKey��
<meta-data
            android:name="io.fabric.ApiKey"
            android:value="593dceb79933219ca082dc4c269d25e712117a78" />
            
�ر���ʾ��twitter Ҫע������˺� fabric�˺���twitter�˺�

��twitter�����˺��½��Լ���Ӧ�ã�����TWITTER_KEY��TWITTER_SECRET��
��activity��ʼ���Ե�¼Ϊ��
private static final String TWITTER_KEY = "ע���key";
private static final String TWITTER_SECRET = "ע���secret";

TwitterAuthConfig authConfig = new TwitterAuthConfig(TWITTER_KEY, TWITTER_SECRET);
Fabric.with(this, new Twitter(authConfig),new TweetComposer());

���Ͼ���ɳ�ʼ���ˣ���Fabric.with()�����ڵ�һ�У�setContentView()֮ǰ��

�����뿴�����ĵ��������Ҫ�� ģ��
https://docs.fabric.io/android/twitter/installation.html


