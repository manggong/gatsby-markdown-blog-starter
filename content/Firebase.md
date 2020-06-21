---
date: 2020-06-19
title: "To create chatting website with firebase"
cover: "https://unsplash.it/400/300/?random?BoldMage"
categories:
  - Firebase
tags:
  - programming
  - Baas
---

## Firebase

1. `Firebase` 홈페이지 접속 후 `Project` 생성
2. 개발 콘솔에서 `Database` 메뉴 이용해서 DB 생성
3. 개발 콘솔에서`Cloud Storage` 활성화
   - 보안정책 기본값으로 설정
4. `Firebase-tools` 설치

```shell
npm -g install firebase-tools
firebase --version
firebase login
firebase use --add // 별칭지정, firebase project 안에서 실행 할 것!!! 생성한 프로젝트 리스트 보임
```

5. `Firebase emulator`

```shell
firebase serve --only hosting
✔  hosting: Local server: http://localhost:5000
```

6. `Firebase SDK` 등록

```html
<script src="/__/firebase/7.15.1/firebase-app.js"></script>
<script src="/__/firebase/7.15.1/firebase-auth.js"></script>
<script src="/__/firebase/7.15.1/firebase-storage.js"></script>
<script src="/__/firebase/7.15.1/firebase-messaging.js"></script>
<script src="/__/firebase/7.15.1/firebase-firestore.js"></script>
<script src="/__/firebase/7.15.1/firebase-performance.js"></script>
<script src="/__/firebase/init.js"></script>
//firebase에 프로젝트의 위치를 알려줌 // 위의 CDN이 있는 곳에서 firbese use
--add 명령어 사용 가능
```

7. `Firebase init` 확인

```javascript
if (typeof firebase === "undefined")
  throw new Error(
    "hosting/init-error: Firebase SDK not detected. You must include it before /__/firebase/init.js"
  );
var firebaseConfig = {
  projectId: "mychat-27f04",
  databaseURL: "https://mychat-27f04.firebaseio.com",
  storageBucket: "mychat-27f04.appspot.com",
  locationId: "us-central",
  apiKey: "YOUR_API_KEY",
  authDomain: "mychat-27f04.firebaseapp.com",
  messagingSenderId: "823556055840",
};
if (firebaseConfig) {
  firebase.initializeApp(firebaseConfig);
}
```

8. 함수정의

```javascript
function signIn() {
  // Sign into Firebase using popup auth & Google as the identity provider.
  var provider = new firebase.auth.GoogleAuthProvider();
  firebase.auth().signInWithPopup(provider);
}

// firebase.auth()로 Oauth 사용
```

9. CR

- Create

```javascript
function saveMessage(messageText) {
  // TODO 7: Push a new message to Firebase.
  return firebase
    .firestore()
    .collection("messages")
    .add({
      name: getUserName(),
      text: messageText,
      profilePicUrl: getProfilePicUrl(),
      timestamp: firebase.firestore.FieldValue.serverTimestamp()
    })
    .catch(function(error) {
      console.error("Error writing new message to database", error);
    });
  // firebase database를 이용해서 collection정의 후 작성
}
```

- Read

```javascript
function loadMessages() {
  // Create the query to load the last 12 messages and listen for new ones.
  var query = firebase.firestore()
                  .collection('messages')
                  .orderBy('timestamp', 'desc')
                  .limit(12);
  
  // Start listening to the query.
  query.onSnapshot(function(snapshot) {
    snapshot.docChanges().forEach(function(change) {
      if (change.type === 'removed') {
        deleteMessage(change.doc.id);
      } else {
        var message = change.doc.data();
        displayMessage(change.doc.id, message.timestamp, message.name,
                       message.text, message.profilePicUrl, message.imageUrl);
      }
    });
  });
}
```





#### Firebase Doc

- [Firebase basic](https://codelabs.developers.google.com/codelabs/firebase-web/?authuser=0#0)

- [REST API Doc](https://firebase.google.com/docs/reference/rest/database)
- 

