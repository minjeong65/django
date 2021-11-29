# 게시물 답글

### Reply 모델

* sub : 답글을 다는 게시물

  * 본문과 댓글은 1:N 관계 => ForeignKey 사용

    > ForeignKey (on_delete 필수 인자 : 본문이 삭제되면 어떻게 할거냐 =>  CASCADE : 같이  사라지도록)

* replyer : 답글 작성자

* comment : 답글 내용



**Error**

```
No Reply matches the given query.
```

