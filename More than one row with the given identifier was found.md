```java
DonationDetail donationDetail = DonationDetail.builder()
                .member(memberService.findOne(request.getMemberId()))
                .post(postService.findOneById(request.getPostId()))
                .donationType(request.getDonationType())
                .donationAmount(request.getDonationAmount())
                .donationDate(request.getDonationDate()).build();
```

프로젝트 진행 중, 게시글 엔티티와 기부 엔티티를 1:1 매핑를 하였다.

기부 API 개발 중, 기부 내역을 새로 만들어 저장하기 위해 위와 같이 만들어 저장하려했다.

하지만 3번 째 줄인, `.post(postService.findOneById(request.getPostId()))` 에서

_\org.springframework.orm.jpa.JpaSystemException: More than one row with the given identifier was found_ 오류가 발생했다.

대충 구글링을 해보니 1:1 매핑 시 발생하는 오류인 거 같은데, stackoverflow에 있는 방법을 적용해도 되지 않는다.

> 해결 시 수정 예정
