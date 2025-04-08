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
crawler.find_element(By.ID, "id_userLoginId").send_keys('lee01020050144@gmail.com')
time.sleep(1)

#비밀번호 입력
crawler.find_element(By.ID, "id_password").send_keys('zxasqw112!@')
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
