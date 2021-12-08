# 게시물 댓글

### Key 추가

* 게시물 별로 id가 필요하듯 댓글별로 id 필요
* 댓글 작성은 게시물 별로 작성하므로 ForeignKey인 pk사용, 댓글 수정/삭제는 primaryKey인 num

</br>

### Reply 모델

* sub : 답글을 다는 게시물

  * 본문과 댓글은 1:N 관계 => ForeignKey 사용

    > ForeignKey (on_delete 필수 인자 : 본문이 삭제되면 어떻게 할거냐 =>  CASCADE : 같이  사라짐

* replyer : 답글 작성자

* comment : 답글 내용

* create_time : 답글 작성일

</br>

### CREATE

* urls : reply/< pk >

</br>

### UPDATE(보류)

* urls : mod_rep/< num >

**Error**

```
NOT NULL constraint failed
```

</br>

### DELETE

* urls : del_rep/< num >

</br>

### 댓글 개수 표시

* 게시물에 댓글이 있는 경우 해당 게시물 제목 옆에 댓글 개수 표시
  * blist : board의 object를 모두 담음
  * i : for 문에서 blist를 순환
  * i.reply_set.count : 게시물 당 댓글 개수

</br>

