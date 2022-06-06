import requests
from bs4 import BeautifulSoup
# from time import sleep
import csv


URL = "https://www.jbiet.edu.in/category.php?mnlnks=6&catid=141"
page = requests.get(URL)
soup = BeautifulSoup(page.content,"html.parser")

result = soup.find("table",class_="table")
table_body = result.find("tbody")

# print(table_body)

table_rows = table_body.find_all("tr")
for each_row in table_rows:
    table_tds = each_row.find_all("td") 
    td_values = []
    for each_td in table_tds:
        td_values.append(each_td.text.strip())
    print(td_values)

    with open('jbit_scrape.csv', 'a') as csvfile:

        csvwriter = csv.writer(csvfile)
        csvwriter.writerow(td_values)
