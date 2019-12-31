---
layout: post
title: Sample-PRJ-RoomAndPaging 기록
categories: [blog, Record]
---
[Sample-PRJ-RoomAndPaging Repository Link (GitHub)](https://github.com/sbean0215/Sample-PRJ-RoomAndPaging)

해당 레포지토리는 Room 과 PagingLibrary 의 기본 사용법 숙지를 위해 진행한 간단한 미니 프로젝트입니다.

처음에는 Room 데이터를 임의로 넣고, 별도 기능없이 화면 하나로 라이브러리 공부만 하려 했었지만, 조금 아쉬워서 FCM 과 추가적인 화면을 더 구성하여 완성하였습니다. 한동안 다른 프로젝트 생성해서 공부하다 재작업하게 되어서, 공부용 프로젝트보다 샘플이나 미니 프로젝트에 가까워졌네요.

<br/>

---
### 함께 사용한 것
프로젝트에 사용한 것들은 다음과 같습니다.

* Java, Android
* Architectural Pattern : MVVM
* Libraris : Dagger2, Databinding, FCM, LiveData

<br/>

---
### 프로토타이핑
![prototyping](/img/posts/2019-12-31-About-Sample-PRJ-RoomAndPaging_kakao_oven.png)

프로토타이핑은 카카오 오븐을 이용했습니다.

카카오 오븐은 생각한 화면을 간단히 그려볼 때 종종 사용합니다. 무료에 웹 기반이라 접근성이 좋아서 사용하게 되었습니다. 아쉬운 점은 가끔 저장했다고 생각했는데 안 되어있어서 작업한 화면이 날아갈 때가 있네요..

<br/>

---
### 기능
![project capture](/img/posts/2019-12-31-About-Sample-PRJ-RoomAndPaging_capture.jpg)

기본적으로 디바이스(Sqlite)에 저장된 유저 리스트를 확인하고, 유저 생성 및 삭제, 해당 유저 id로 수신된 FCM 메세지를 볼 수 있습니다.

**FCM 메세지 전송시 구조**
```
{
  "message":{
    "token":"bk3RNwTe3H0:CI2k_HHwgIpoDKCIZvvDMExUdFQ3P1...",
    "data":{
      "target_user_id" : "3",
      "msg_type" : "AD",
      "contents" : "Blah blah"
    }
  }
}
```

<br/>

---
### 기타 구현 기능

#### 1. 아이템 선택기능
어떤 유저를 삭제 또는 FCM을 확인할 수 있도록, 유저 리스트에서 하나의 유저를 선택하고 선택된 아이템의 모양을 변경시켰습니다.

만들때 Selection 의 존재를 몰랐기 때문에, @Entity 클래스에 @Ignore 어노테이션을 사용하여 bool isSelected 을 추가하고 또한 Adapter Class 에서 선택된 User 를 들고있는 방식으로 구현했습니다. ViewHolder 에서 setBackground 를 했을 경우 해당 Item 재사용시 문제가 생긴 경험이 있어, DataBinding 을 사용하여 백그라운드 처리를 해주었습니다.

다음번에는 Selection 으로 구현하도록 합시다..

#### 2. 탭 레이아웃, 커스텀 탭
탭 레이아웃과 뷰페이저를 연결해주고(탭 선택 <--연결--> 페이지 변경), 커스텀 탭을 설정해주었습니다.

커스텀 탭은 탭이 TabLayout 에 추가된 후 tabLayout.getTabAt(position).setCustomView(CustomlayoutId) 로 설정할 수 있습니다. xml 작성시 별 생각없이 Tablayout 의 안쪽에 TabItem을 넣어뒀다가 getTabAt 에서 엉뚱한 TabItem 이 튀어나와 한참 헤메었네요.

새 메세지(읽지않은) 수를 세어서 탭 위에 표시되도록 처리하였습니다.

<br/>

---
### 마무리

간단히 해봐야지 하고 시작했는데 생각보다 시간이 좀 걸렸네요. 그래서 처음에 생각했던 랜덤 이미지 추가, 노티알람 표시는 구현하지 않고, Room과 PagingLibrary 실습에 집중하여 마무리 하게 되었습니다.

늘 느꼈지만 알고 있었던 것, 해봤었던 것들도 다시 해보면 여러가지 고민할 점들이 있네요. 그래서 이번엔 간단한 내용들이나마 간단하게 기록을 남겨보았습니다. 좀 더 완성도 있는 글이나 프로젝트 소개를 작성하도록 노력해야겠습니당. 그리고 코드리뷰 해주신 박** 선배님 넘나 감사드립니다 XD !!
