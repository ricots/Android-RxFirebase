[![Hex.pm](https://img.shields.io/hexpm/l/plug.svg)](http://www.apache.org/licenses/LICENSE-2.0) [![Platform](https://img.shields.io/badge/platform-android-green.svg)](http://developer.android.com/index.html)
[ ![Download](https://api.bintray.com/packages/ezhome/maven/rxfirebase/images/download.svg) ](https://bintray.com/ezhome/maven/rxfirebase/_latestVersion)
[![CircleCI](https://circleci.com/gh/ezhome/Android-RxFirebase.svg?style=shield)](https://circleci.com/gh/ezhome/Android-RxFirebase)

# RxFirebase

RxJava implementation by ezhome for the Android [Firebase client](https://www.firebase.com/docs/android/).

----
Contents
--------
- [Usage](#usage)
- [Download](#download)
- [Tests](#tests)
- [Code style](#code-style)
- [License](#license)

Usage
-----

```java
    final Firebase firebaseRef = new Firebase("https://docs-examples.firebaseio.com/web/saving-data/fireblog/posts");
    RxFirebase.getInstance().observeValueEvent(firebaseRef).subscribe(new GetPostsSubscriber());
  
    private final class GetPostsSubscriber extends Subscriber<DataSnapshot> {
      @Override public void onCompleted() {
        PostsFragment.this.showProgress(false);
      }
    
      @Override public void onError(Throwable e) {
        PostsFragment.this.showProgress(false);
        PostsFragment.this.showError(e.getMessage());
      }
    
      @SuppressWarnings("unchecked") @Override public void onNext(DataSnapshot dataSnapshot) {
        List<BlogPostEntity> blogPostEntities = new ArrayList<>();
        for (DataSnapshot childDataSnapshot : dataSnapshot.getChildren()) {
          blogPostEntities.add(childDataSnapshot.getValue(BlogPostEntity.class));
        }
        PostsFragment.this.renderBlogPosts(blogPostEntities);
      }
    }
```     

Check the example application [here](https://github.com/ezhome/Android-RxFirebase/tree/master/app)

Download
--------
The project is available on jCenter. In your app build.gradle (or explicit module) you must add this:
```
dependencies {
  compile 'com.ezhome:rxfirebase:1.0.0'
}
```


Tests
-----

Tests are available in `rxfirebase/src/test/java/` directory and can be executed from Android Studio or CLI with the following command:

```
./gradlew test
```

Code style
----------

Code style used in the project is called `SquareAndroid` from Java Code Styles repository by Square available at: https://github.com/square/java-code-styles.


License
-------

    Copyright 2016 Ezhome Inc.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.