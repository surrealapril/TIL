# MyBatis foreach, parameterType List,Model,Map

```
<insert id="insert"parameterType="java.util.List">
 INSERT INTO 테이블 VALUES
 (
    <foreach collection="list" item="item" separator=",">
        #{item.baseDate}, #{item.baseTime}, #{item.category},
        #{item.fcstDate}, #{item.fcstTime}, #{item.fcstValue}
    </foreach>
 )
</insert>
 ```

 collection="list" item="item" default.

 # #{} ${} 차이
 #{} : 데이터 자체를 문자열로 인식해서 ' '가 생김
 ${} : 데이터 값 그대로 전달. ' ' 없음. ${} 는 SQL injection 문제에 취약

 방금 INSERT 된 Seq 가져오기
```
 <insert id="insertData" parameterType="DataClass" useGeneratedKeys="true"   keyProperty="id">
     /* query */
</insert>
```

 [참조링크]
https://myeongdev.tistory.com/30?category=1009844
https://kimsg.tistory.com/255?category=712079
