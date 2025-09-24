# K-POP Fandom Wiki API를 활용한 Crawler 사용법

## csv 파일 내보내기
[주의사항]
- 맨 상단의 "필수 실행 코드" 에서 의존성 관리, 오늘 날짜 폴더 생성 선 진행되야함
  
**_Group 정보 내보내기_**
- Group Crawling 목차 안의 KpopGroupCrawler_memberDict 클래스 실행
- 아래의 코드 차례로 실행
```python
crawler = KpopGroupCrawler_memberDict() # 크롤러 객체 생성
# boy 그룹 내보내기
boy_groups = ["NCT", "BTS", "Stray_Kids", "SEVENTEEN", "NEEZ"]

# 데이터프레임 변수명, 그룹 내 멤버 정보 모아둘 변수명 = crawler.create_csv_from_groups(그룹 리스트, "저장될 파일명", "group type 에 들어갈 값")
df_boy_group, boy_groups_member_pages = crawler.create_csv_from_groups(boy_groups, "groups_info_boy.csv", "Boy Group")
```
[주의사항]
- 그룹명 리스트는 https://kpop.fandom.com 내의 url 에 사용되는 그룹명이 들어가야함
- 해당 그룹의 유닛 그룹까지 한번에 크롤링됨 (ex : 'NCT' 크롤링하면서 'NCT 127', 'NCT DREAM', 'NCT WISH' 등 모두 크롤링됨)
- 동일 그룹명 입력하여도 중복 없이 1번만 크롤링됨
- 그룹명 존재하지 않음 등의 이유로 크롤링 실패시 null 값으로 데이터 추가됨
- group type 은 선택적인 파라미터로 입력 안하면 null 값이 들어감
- 그룹 내 멤버 리스트 추출됨 (탈퇴 멤버 제외됨)
- 본진 그룹과 유닛에 중복적으로 멤버가 있어도 1번만 리스트업됨 (ex : 'NCT' 의 Mark 멤버 리스트에 저장 -> 'NCT 127' 의 Mark 이미 멤버 리스트에 저장되어 있으므로 추가안됨)

**_Artist 정보 내보내기_**
- Artist Crawling 목차 안의 코드 셀 실행
- 아래의 코드 차례로 실행
```python
# 데이터프레임 저장할 변수명 = create_artist_csv(함수명) (Group 정보 내보내기에서 저장한 멤버 정보가 담긴 변수, "저장될 파일명")
artist_df_boy = create_artist_csv(boy_groups_member_pages, "artists_boy_group.csv")
```
[주의사항]
- Group 정보 내보내기 먼저 실행 후 Aritst 내보내기 실행되야함
