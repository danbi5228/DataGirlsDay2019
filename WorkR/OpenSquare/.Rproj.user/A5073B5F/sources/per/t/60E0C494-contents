# 공유 자전거 대여 현황
#  데이터: 서울 열린데이터광장
# 서울특별시 공공 자전거 대여소 정보
# 서울특별시 공공 자전거 이용정보(월별)

library(readxl)
station<-read_excel("서울시 공공자전거 대여소 설치 일시 정보(20190517).xlsx")
View(station)
bike<-read_excel("서울특별시 공공자전거 시간대별 대여정보_201811.xlsx")
View(bike)

# 전처리
install.packages("dplyr")
library(dplyr)

# bike 데이터에 2018년 데이터가 전부 있다고 가정
# %>% :bike에서 filtering해라 라는 의미로, dplyr에서 제공하는 method
bike201811<-bike %>% filter(대여일자 == 201811)

bike <- bike %>% select(대여소번호,대여소명,이용건수)

# 1번 column명만 바꾸고 싶은 경우
names(bike)[1] <- '대여소ID'
station <- station %>% select(대여소ID, 위도, 경도, 거치대수)
View(station)

# 테이블 합치기
result<-merge(bike, station, by='대여소ID')
View(result)

# 시각화 - 지도 관련
install.packages("leaflet") # 설치
library(leaflet) # 해당 라이브러리를 쓴다고 선언

leaflet(data=result) %>% addTiles() %>%
  addMarkers(result$경도, result$위도, 
             popup=as.character(result$거치대수),
             label=as.character(result$대여소명))

# 마커를 circle로
leaflet(data=result) %>%
  addTiles() %>%
  addCircleMarkers(~경도, ~위도, radius = ~대여건수/100,
                   popup=~as.character(거치대수), 
                   label=~as.character(대여소명))