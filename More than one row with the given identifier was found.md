```java
DonationDetail donationDetail = DonationDetail.builder()
                .member(memberService.findOne(request.getMemberId()))
                .post(postService.findOneById(request.getPostId()))
                .donationType(request.getDonationType())
                .donationAmount(request.getDonationAmount())
                .donationDate(request.getDonationDate()).build();
```

프로젝트 진행 중, 게시글 엔티티와 기부내역 엔티티를 1:1 매핑를 하였다.

기부 API 개발 중, 기부 내역을 새로 만들어 저장하기 위해 위와 같이 만들어 저장하려했다.

하지만 3번 째 줄인, `.post(postService.findOneById(request.getPostId()))` 에서

_\org.springframework.orm.jpa.JpaSystemException: More than one row with the given identifier was found_ 오류가 발생했다.

대충 구글링을 해보니 1:1 매핑 시 Hibernate는 단일 결과를 기대하였지만, 실제 결과는 2개 이상의 결과가 반환되어 생기는 오류라고 한다.

# 해결

ERD 설계, 매핑 관계부터 차근차근 보다가 1:1 양방향과 단방향에 대해 생각해보았다.

뭔가 양방향으로 매핑이 되어 있기에 참조할 때 중복이 되지 않을까? 싶은 심증에 단방향 매핑으로 바꾸어보니 이상없이 값이 저장된다.

아직 정확한 원인과 해결 과정에 대해서는 모르니까 JPA 공부하면서 다시 적기로 한다.
