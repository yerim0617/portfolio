# portfolio
웹크롤링, 추천 알고리즘 코드 저장

```python

##웹 크롤링 코드
pip install selenium
pip install chromedriver-autoinstaller

from selenium import webdriver
import chromedriver_autoinstaller
import time
import pandas as pd
import urllib.request
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By

chrome_ver = chromedriver_autoinstaller.get_chrome_version().split('.')[0]
print(chrome_ver)

try:
    crawler = webdriver.Chrome(f' ./{chrome_ver}/chromedriver.exe')
except:
    chromedriver_autoinstaller.insrall(True)
    crawler = webdriver.Chrome(f' ./{chrome_ver}/chromedriver.exe')
crawler.implicitly_wait(10)
crawler.get('https://www.netflix.com/kr/login')

#로그인 과정
#아이디 입력
crawler.find_element(By.ID, "id_userLoginId").send_keys('사용자 아이디')
time.sleep(1)

#비밀번호 입력
crawler.find_element(By.ID, "id_password").send_keys('비밀번호')
time.sleep(1)

#로그인 버튼 클릭
crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div[3]/div/div/div[1]/form/button').click()
time.sleep(1)

#프로필 클릭
crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[1]/div[2]/div/div/ul/li[4]/div/a/span').click()
time.sleep(1)



#정보 가져오기

names= []
descriptions= []
genres= []
images= []
links = []

before_h = crawler.execute_script("return window.scrollY")
       
#스크롤 내리기 (콘텐츠 로딩을 위해 맨 아래까지 스크롤 내리기)
while True:
    crawler.find_element(By.CSS_SELECTOR, 'body').send_keys(Keys.END)
    time.sleep(2)
    after_h = crawler.execute_script("return window.scrollY")
    if after_h == before_h:
        break
    before_h = after_h
   
#이름, 설명, 장르 가져오기
for row in range(0,3):
    for div in range(1,6):
        crawler.find_element('xpath', '//*[@id="row-{}"]/div/div/div/div/div/div[{}]'.format(row,div)).click()
        time.sleep(3)
        try:
            name = crawler.find_element(By.TAG_NAME, "strong").text
            names.append(name)
            time.sleep(1)
        except:
            name = crawler.find_element(By.CSS_SELECTOR, 'episodeSelector-season-name').text
            names.append(name)
            time.sleep(1)
        description = crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[3]/div/div[1]/div/div/div[1]/p').text
        descriptions.append(description)
        time.sleep(1)
        genre = ("애니메이션")
        genres.append(genre)
        time.sleep(1)
        crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[2]').click()
        time.sleep(2)
       
for row in range(0,3):
    for div in range(0,5):
        link = crawler.find_element('xpath', '//*[@id="title-card-{}-{}"]/div[1]/a'.format(row,div)).get_attribute("href")
        links.append(link)

#이름, 설명, 장르 가져오기
for row in range(3,6):
    for div in range(1,6):
        crawler.find_element('xpath', '//*[@id="row-{}"]/div/div/div/div/div/div[{}]'.format(row,div)).click()
        time.sleep(3)
        try:
            name = crawler.find_element(By.TAG_NAME, "strong").text
            names.append(name)
            time.sleep(1)
        except:
            name = crawler.find_element(By.CSS_SELECTOR, 'episodeSelector-season-name').text
            names.append(name)
            time.sleep(1)
        description = crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[3]/div/div[1]/div/div/div[1]/p').text
        descriptions.append(description)
        time.sleep(1)
        genre = ("애니메이션")
        genres.append(genre)
        time.sleep(1)
        crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[2]').click()
        time.sleep(2)
       
for row in range(3,6):
    for div in range(0,5):
        link = crawler.find_element('xpath', '//*[@id="title-card-{}-{}"]/div[1]/a'.format(row,div)).get_attribute("href")
        links.append(link)


#이름, 설명, 장르 가져오기
for row in range(6,9):
    for div in range(1,6):
        crawler.find_element('xpath', '//*[@id="row-{}"]/div/div/div/div/div/div[{}]'.format(row,div)).click()
        time.sleep(3)
        try:
            name = crawler.find_element(By.TAG_NAME, "strong").text
            names.append(name)
            time.sleep(1)
        except:
            name = crawler.find_element(By.CSS_SELECTOR, 'episodeSelector-season-name').text
            names.append(name)
            time.sleep(1)
        description = crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[3]/div/div[1]/div/div/div[1]/p').text
        descriptions.append(description)
        time.sleep(1)
        genre = ("애니메이션")
        genres.append(genre)
        time.sleep(1)
        crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[2]').click()
        time.sleep(2)
       
for row in range(6,9):
    for div in range(0,5):
        link = crawler.find_element('xpath', '//*[@id="title-card-{}-{}"]/div[1]/a'.format(row,div)).get_attribute("href")
        links.append(link)


#이름, 설명, 장르 가져오기
for row in range(9,12):
    for div in range(1,6):
        crawler.find_element('xpath', '//*[@id="row-{}"]/div/div/div/div/div/div[{}]'.format(row,div)).click()
        time.sleep(3)
        try:
            name = crawler.find_element(By.TAG_NAME, "strong").text
            names.append(name)
            time.sleep(1)
        except:
            name = crawler.find_element(By.CSS_SELECTOR, 'episodeSelector-season-name').text
            names.append(name)
            time.sleep(1)
        description = crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[3]/div/div[1]/div/div/div[1]/p').text
        descriptions.append(description)
        time.sleep(1)
        genre = ("애니메이션")
        genres.append(genre)
        time.sleep(1)
        crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[2]').click()
        time.sleep(2)
       
for row in range(9,12):
    for div in range(0,5):
        link = crawler.find_element('xpath', '//*[@id="title-card-{}-{}"]/div[1]/a'.format(row,div)).get_attribute("href")
        links.append(link)


#이름, 설명, 장르 가져오기
for row in range(12,15):
    for div in range(1,6):
        crawler.find_element('xpath', '//*[@id="row-{}"]/div/div/div/div/div/div[{}]'.format(row,div)).click()
        time.sleep(3)
        try:
            name = crawler.find_element(By.TAG_NAME, "strong").text
            names.append(name)
            time.sleep(1)
        except:
            name = crawler.find_element(By.CSS_SELECTOR, 'episodeSelector-season-name').text
            names.append(name)
            time.sleep(1)
        description = crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[3]/div/div[1]/div/div/div[1]/p').text
        descriptions.append(description)
        time.sleep(1)
        genre = ("애니메이션")
        genres.append(genre)
        time.sleep(1)
        crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[2]').click()
        time.sleep(2)
       
for row in range(12,15):
    for div in range(0,5):
        link = crawler.find_element('xpath', '//*[@id="title-card-{}-{}"]/div[1]/a'.format(row,div)).get_attribute("href")
        links.append(link)

#이름, 설명, 장르 가져오기
for row in range(15,18):
    for div in range(1,6):
        crawler.find_element('xpath', '//*[@id="row-{}"]/div/div/div/div/div/div[{}]'.format(row,div)).click()
        time.sleep(3)
        try:
            name = crawler.find_element(By.TAG_NAME, "strong").text
            names.append(name)
            time.sleep(1)
        except:
            name = crawler.find_element(By.CSS_SELECTOR, 'episodeSelector-season-name').text
            names.append(name)
            time.sleep(1)
        description = crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[3]/div/div[1]/div/div/div[1]/p').text
        descriptions.append(description)
        time.sleep(1)
        genre = ("애니메이션")
        genres.append(genre)
        time.sleep(1)
        crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[2]').click()
        time.sleep(2)
       
for row in range(15,18):
    for div in range(0,5):
        link = crawler.find_element('xpath', '//*[@id="title-card-{}-{}"]/div[1]/a'.format(row,div)).get_attribute("href")
        links.append(link)

#이름, 설명, 장르 가져오기
for row in range(18,21):
    for div in range(1,6):
        crawler.find_element('xpath', '//*[@id="row-{}"]/div/div/div/div/div/div[{}]'.format(row,div)).click()
        time.sleep(3)
        try:
            name = crawler.find_element(By.TAG_NAME, "strong").text
            names.append(name)
            time.sleep(1)
        except:
            name = crawler.find_element(By.CSS_SELECTOR, 'episodeSelector-season-name').text
            names.append(name)
            time.sleep(1)
        description = crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[3]/div/div[1]/div/div/div[1]/p').text
        descriptions.append(description)
        time.sleep(1)
        genre = ("애니메이션")
        genres.append(genre)
        time.sleep(1)
        crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[2]').click()
        time.sleep(2)
       
for row in range(18,21):
    for div in range(0,5):
        link = crawler.find_element('xpath', '//*[@id="title-card-{}-{}"]/div[1]/a'.format(row,div)).get_attribute("href")
        links.append(link)

#이름, 설명, 장르 가져오기
for row in range(21,23):
    for div in range(1,6):
        crawler.find_element('xpath', '//*[@id="row-{}"]/div/div/div/div/div/div[{}]'.format(row,div)).click()
        time.sleep(3)
        try:
            name = crawler.find_element(By.TAG_NAME, "strong").text
            names.append(name)
            time.sleep(1)
        except:
            name = crawler.find_element(By.CSS_SELECTOR, 'episodeSelector-season-name').text
            names.append(name)
            time.sleep(1)
        description = crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[3]/div/div[1]/div/div/div[1]/p').text
        descriptions.append(description)
        time.sleep(1)
        genre = ("애니메이션")
        genres.append(genre)
        time.sleep(1)
        crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[2]').click()
        time.sleep(2)
       
for row in range(21,23):
    for div in range(0,5):
        link = crawler.find_element('xpath', '//*[@id="title-card-{}-{}"]/div[1]/a'.format(row,div)).get_attribute("href")
        links.append(link)


for div in range(1,4):
    crawler.find_element('xpath', '//*[@id="row-23"]/div/div/div/div/div/div[{}]'.format(div)).click()
    time.sleep(3)
    name = crawler.find_element(By.TAG_NAME, "strong").text
    names.append(name)
    description = crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[3]/div/div[1]/div/div/div[1]/p').text
    descriptions.append(description)
    time.sleep(1)
    genre = ("애니메이션")
    genres.append(genre)
    time.sleep(1)
    crawler.find_element('xpath', '//*[@id="appMountPoint"]/div/div/div[1]/div[2]/div/div[2]').click()
    time.sleep(2)

for div in range(0,3):
    link = crawler.find_element('xpath', '//*[@id="title-card-23-{}"]/div[1]/a'.format(div)).get_attribute("href")
    links.append(link)


df = pd.DataFrame({'name':names, 'description':descriptions, 'genre':genres, 'link': links})
print(df)

##추천 알고리즘 코드 (유사한 작품도 같이 띄워주면 기능적으로 더 이득을 가져갈 것 같다라는 팀원들 간의 회의 끝에 추천 알고리즘 작성하기로 결정)

# 구글 드라이브 연동
from google.colab import drive
drive.mount('/content/drive')

# 필요 라이브러리 임포트
import pandas as pd
import numpy as np
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

# 데이터 로드 및 전처리
file_path = "/content/drive/MyDrive/졸작/contents_drama.csv"
chunk_size = 1000

data_combined = pd.DataFrame()
for chunk in pd.read_csv(file_path, encoding='cp949', chunksize=chunk_size, na_filter=False):
    chunk_data = chunk[['name', 'description', 'genre']]
    chunk_data_cleaned = chunk_data.dropna(subset=['name', 'description', 'genre'])
    chunk_data_cleaned = chunk_data_cleaned.assign(
        combined_features=chunk_data_cleaned['genre'] + ' ' + chunk_data_cleaned['description']
    )
    data_combined = pd.concat([data_combined, chunk_data_cleaned])

# TF-IDF 및 코사인 유사도
tfidf = TfidfVectorizer(stop_words='english')
tfidf_matrix = tfidf.fit_transform(data_combined['combined_features'])
cosine_sim = cosine_similarity(tfidf_matrix, tfidf_matrix)

# 추천 함수
def recommend_content_list(name, cosine_sim, data):
    indices = pd.Series(data.index, index=data['name']).drop_duplicates()
    idx = indices[name]
    sim_scores = list(enumerate(cosine_sim[idx]))
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)[1:11]
    content_indices = [i[0] for i in sim_scores]
    return data['name'].iloc[content_indices]

# 예시 실행
recommendations = recommend_content_list('보이스', cosine_sim, data_combined)
print(recommendations)

