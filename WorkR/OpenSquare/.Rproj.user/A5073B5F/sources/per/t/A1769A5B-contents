# 서울시 구별 인구수를 가져와보자
# 열린서울데이터광장
# 약간의 데이터 전처리과정 및 시각화를 경험

data <- read.csv("")

# excel를 읽을 수 있는 라이브러리 설치
# 파일마다 install 해주어야한다
install.packages("readxl") 

library(readxl) # 설치된 readxl을 가져오기

jumin<-read_excel("peopleSeoul.xls")
View(jumin)

# 전처리 (내가 필요한 데이터만 뽑아내는 것)
# '열' 에 들어갈 내용이 많으므로 combine으로 감싼다
jumin<-jumin[ , c(2, 4, 7, 10, 14)] 

# 열 개수와 맞춰서 덮어씌운다
names(jumin)<-c('구별', '인구수', '한국인', '외국인', '고령자')

# 1행부터 3행까지 삭제
jumin <- jumin[-c(1:3),]

str(jumin)

# 인구수 컬럼의 타입이 character니까 하나씩 가져와서 numeric으로 변환
# 이후 덮어쓰기 
jumin$인구수<-as.numeric(as.character(jumin$인구수))
jumin$한국인<-as.numeric(as.character(jumin$한국인))
jumin$외국인<-as.numeric(as.character(jumin$외국인))
jumin$고령자<-as.numeric(as.character(jumin$고령자))
str(jumin)

#Q. 전체 인구수에서 외국인의 비율을 알고싶다!

#df이름$컬럼명 : 해당 컬럼명이 없으면 새로 만들어준다!
jumin$외국인비율 <- jumin$외국인/jumin$인구수 * 100
View(jumin)

#외국인 비율 값이 소수점 2개까지만 나오도록
#digit = -2 : 백 단위에서 반올림 ?
jumin$외국인비율 <- round(jumin$외국인/jumin$인구수 * 100, digit = 2)
jumin$외국인비율 <- round(jumin$외국인비율, digit = 2)

#시각화 라이브러리 : ggplot2
# bar / line / point
install.packages("ggplot2")
library(ggplot2)

# +기호를 위에 두고 줄바꿈을 하는건 괜찮지만 +기호가 함께 줄바꿈되면 error
ggplot(jumin, aes(x=구별, y=인구수)) + 
  geom_bar(fill='blue', stat = 'identity')

ggplot(jumin, aes(x=인구수, y=외국인)) + geom_point()




