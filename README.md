from selenium import webdriver
#from selenium.webdriver.common.keys import Keys
#from selenium.webdriver.common.desired_capabilities import DesiredCapabilities
import xlsxwriter

workbook = xlsxwriter.Workbook('myDB.xlsx')
worksheet = workbook.add_worksheet()

driver = webdriver.Firefox()
driver.implicitly_wait(10)
driver.get("https://tengrinews.kz/kazakhstan_news/skolko-stoit-obuchenie-v-nazarbaev-universitete-303147/")
driver.execute_script("window.scrollTo(0,document.body.scrollHeight);")

title = driver.find_elements_by_tag_name('h1')
authors = driver.find_elements_by_xpath('//div[@class="comment"]/div[@class="user"]/span')
comments = driver.find_elements_by_xpath('//div[@class="comment"]/div[@class="comment_text"]/span[@class="substr"]') 
ratings = driver.find_elements_by_xpath('//div[@class="comment"]/div[@class="rating"]/span[@class="rate plus"]')
dates = driver.find_elements_by_xpath('//div[@class="comment"]/div[@class="date"]')


for i in range(0, 4):
	if i ==0:
		worksheet.write_column(0, i, title[0].text)
	elif i==1:
		worksheet.write_column(0, i, authors[i].text)
	elif i==2:
		worksheet.write_column(0, i, comments[i].text)
	elif i==3:
		worksheet.write_column(0, i, dates[i].text)	
workbook.close()

#for i in range(0, len(authors)):
#	if i<1:
#		print(title[i].text)
#		for j in range(0, 6):
#				print("%s   %s" % (authors[j].text, comments[j].text))
