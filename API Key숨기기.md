#API Key 숨기기

API Key는 config.properties에 따로 관리
root-context.xml 파일 수정하여 properties 추가
> <util:properties id="config" location="/properties/*.properties"/> <context:property-placeholder properties-ref="config"/>

config.properties 에 api-key 추가

Controller에서 key값 가져오는 방법 
@Value("#{properties이름['가져올 값 이름']})
private String 변수명;

날씨 API 크롤링 프로젝트에서 ApiKey를 null로 받아온 이유 
    - config.properties 경로 제대로 적어주기(폴더 적기)
log로 ApiKey를 제대로 받아온 걸 확인했지만 샘플 코드에서 service error뜬 이유
    - 내가 사용한 건 이미 UTF-8로 인코딩 된 키를 사용해서 -> 디코딩 키를 사용하니 해결


