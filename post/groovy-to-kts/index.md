---
layout: post
title:  "Kotlin DSL 적용하며 발생한 문제"
subtitle: "무수한 빨간 줄이 나에게 준 고통"
type: "Kotlin"
post: true
text: true
author: "stitch"
post-header: true
order: 1
---

# Groovy에서 KTS로 빌드 구성 이전

[Migrate your build configuration from Groovy to KTS](https://developer.android.com/studio/build/migrate-to-kts?hl=ko)을 통해 gradle.build에서 gradle.build.kts 를 적용하면서 발생한 문제에 대해 공유합니다.


KTS로 구성하는 과정를 BuildSrc와 Version Catalog를 통한 버전 관리를 진행했다. 더욱 신기했던 것은 Build는 정상적으로 작동했다. `Invalide Caches`와 `Clean Project`를 진행해도 무수한 빨간 에러는 제거되지 않았습니다.
정확히 원인을 파악하지 못해서 계속해서 진행했는데 해결되지 않았고 30분 ~ 1시간 가량을 투자했습니다.

### 원인

```
Cannot access 'java.lang.Object' which is a supertype of 'org.gradle.api.initialization.resolve.
DependencyResolutionManagement'. Check your module classpath for missing or conflicting dependencies
```

빌드하는 과정 속인 인덱싱을 하는 도중에 발생한 원인으로 보인다. 해결 방법은 크게 2가지로 나타나는 것 같습니다.

첫 번째 방법은 해당 프로젝트의 `.idea` 파일을 지우는 방법이다. 필자는 이 방법으로 해결되지 않아서 두 번째 방법을 해결했습니다.

두 번째 방법은 `Library/Caches/Google/AndroidStudioPreview2022.3/caches` 파일을 지우는 것입니다.

`Invalide Caches`와 `Clean Project`을 하면서 해결하신 분들도 계신데 두 번째 방법으로 해결된 이유를 생각해보면, 안드로이드 스튜디오에서 자체적으로 캐시를 제거하지 못했던 것 같다. 새로운 것을 알 수 있어서 좋았지만, 다른 분들은 많은 시간을 소모하지 않길 바래서 작성합니다.