# 추천

### 게시물 추천

* 모델 변경
  * voter = models.ManyToManyField(User)
  
* url 추가

  * voter/< pk >

* b.voter.add(request.user) : 추천

* 추천은 한 번만 누를 수 있도록 함

  ```python
  if request.user in b.voter.all():
  	return redirect('board:detail', pk=pk)
  ```

* b.voter.count : 추천수

* 게시글 왼쪽에 추천 버튼 생성 및 제목 옆에 추천수 표시

