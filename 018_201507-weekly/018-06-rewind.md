# rewind

- 페이지 링크: https://github.com/gilesbowkett/rewind

우왔!! 깃 히스토리 분석 스크립트랍니다.

(*뭐 무슨 블로그에서 영향을 받았고, 무슨 책에 자세히 설명되어 있다고 하는데
영상이나 책이 중요한건 아니고, 자세히 설명 되어 있지도 않네요.*)
Git 프로젝트의 의미있는 이력을 빠르게 만들고 싶을 때 사용하라고 합니다.

그런데 재밌네요. 스타가 총 1500개정도 되는데 이번 주에만 1360개의 스타를 받았습니다. 이 프로젝트는 지난 해 전혀 활동도 없었거든요.
이슈는 물론 PU조차 전혀 반응이 없었습니다. 그런데 왜 갑자기 스타를 엄청나게 받았을까요?

하도 궁금해서 원 저자한테 메일로 물어봤죠.

그랬더니 대답이 [해커뉴스](https://news.ycombinator.com/)라는 곳에 관련 글이 있길래 
이 프로젝트를 언급했더니 그랬다고 하네요.
어쨌건 이 프로젝트가 트렌드에 올라왔으니, 뭔지 한번 살펴 볼까요.

프로젝트를 보면 파일이 몇개 있습니다. 실행파일은 bash_shell과 Ruby 스크립트구요. 
( *윈도우에서는 실행하기 귀찮겠네요* )

```
// Git 리파지토리 통계 분석
file_stats.sh
// 저자가 누군지 찾기
determine_authors.sh
merge-hashes.rb
tally_authors.rb
the-hashes.rb
```



##### 일단 Git 리파지토리 통계를 내볼까요.
각 파일마다 라인수, 커밋 수, 최초커밋 날짜와 마지막 커밋날짜를 CSV파일로 만들어줍니다.
(*이게 무슨의미가 있을까요??*)

```
$ sh file_stats.sh [경로] [파일종류들] > stats.csv
```

위의 명령어로 실행하면 아래와 같이 CSV 파일로 결과를 보여줍니다. 
```
filename,lines of code,number of commits,date of first commit,date of last commit
./tally_authors.rb,22,1,Apr 9 2013,Apr 9 2013
./merge-hashes.rb,14,1,Jul 21 2014,Jul 21 2014
./the-hashes.rb,15,1,Jul 21 2014,Jul 21 2014
```


##### 다음은 원작자 찾기
처음에 프라지토리의 원작자가 될법한 이벤트를 세구요. 그리고 나서 이름순으로 정렬을 해 준뎁니다.
위에 통계 낼때 사용했던 file_stats.sh의 경우 여러종류의 파일을 한꺼번에 수행할 수 있지만,
두번째 원작자 찾기는 한번에 하나의 종류만 수행할 수 있다고 합니다. 이거 고친 풀리퀘스트는 환영한합니다.
그리고 아주 큰 프로젝트나 히스토리가 엄청 큰 경우 아주 느릴 수 있다네요.

실행 방법이 좀 복잡하네요. 프로젝트 경로와 determine_authors.sh의 경로 그리고 파일 확장자를 
정해 주면 됩니다. ( *몇년째 진행중인 프로젝트에서 js파일을 대상으로 돌리니 진짜로 한참걸리네요* )
```
ruby tally_authors.rb <(cd /project && /this_dir/determine_authors.sh "js")
```

결과는 
```
{
        "ciro" => 2,
       "karlo" => 3,
     "dmitriy" => 11,
        "depa" => 5,
       "riyad" => 1,
       "randx" => 3,
      "robert" => 2,
        "koen" => 2,
       "nihad" => 1,
    "patricio" => 1
}

```
요렇게 보여줍니다. 누가 커밋을 몇번했는지 찾아서 카운팅 해주는게 다 인거 같아요. 저 결과대로 라고 하면 
dmitriy가 원작자라고 판단해야 하는걸까요? 


###### 근데 프로젝트 이름이 왜 리와인드 일까요? 리와인드가 지금 트랜스포머 만화의 주인공 이랩니다. 하하 :smile: