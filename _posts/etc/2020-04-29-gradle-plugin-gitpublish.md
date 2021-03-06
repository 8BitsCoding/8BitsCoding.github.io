---
title: "Gradle - plugin : gitpublish"
permalink: gradle/plugin/gitpublish/                # link 직접 지정
toc: true                       # for Sub-title (On this page)
comments: true                  # for disqus Comments
categories:                     # for categories
date: 2020-04-29 00:00:00 -0000
last_modified_at: 2020-04-29 00:00:00 -0000
sidebar:
  title: "etc"
  nav: etc
---

```groovy
// for git publish plugin
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'org.ajoberstar:gradle-git-publish:2.1.1'
    }
}

apply plugin: 'org.ajoberstar.git-publish'

gitPublish {
    // where to publish to (repo must exist)
    repoUri = ''
    // git 주소 입력
 
    branch = 'master'
    // branch 입력

    repoDir = file("D:/temp/personal_repo_for_mywiki_temp") // defaults to $buildDir/gitPublish
    // 로컬의 디렉터리를 여기로 쓰겠다

    contents {
        from 'D:/temp/personal_repo_for_mywiki'
        // 어디서 복사해 올지
    }

    preserve {
        //include '**/**'
        exclude '**/**'
        // 로컬의 디렉터리 중 어떤파일을 추가하고 어떤파일을 제외할지?
        // 결국은 복사해올 폴더꺼를 다 쓸거기 때문에 모두 exlucde함.
    }

    commitMessage = 'Gradle git publish test...' // defaults to 'Generated by gradle-git-publish'
    // commit Message 입력
}
```

스크립트는 아래와 같이 입력해야 git의 id, password를 넣을 수 있다.

```s
gradle gitPublishPush -Dorg.ajoberstar.grgit.auth.username=<id> -Dorg.ajoberstar.grgit.auth.password=<password>
```
 
* [참고사이트](https://github.com/ajoberstar/gradle-git-publish)