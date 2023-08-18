# thursday230817_repo
import requests
from bs4 import BeautifulSoup

# Function to get quotes from a page
def get_quotes(url):
    response = requests.get(url)
    if response.status_code != 200:
        print(f"Failed to retrieve the page with status code: {response.status_code}")
        return []

    soup = BeautifulSoup(response.content, 'html.parser')
    quotes_divs = soup.find_all("div", class_="quote")

    quotes = []
    for quote_div in quotes_divs:
        text = quote_div.find("span", class_="text").text
        author = quote_div.find("span", class_="author").text
        quotes.append((text, author))

    return quotes

if __name__ == "__main__":
    URL = "http://quotes.toscrape.com/page/1/"
    quotes = get_quotes(URL)

    if quotes:
        for quote, author in quotes:
            print(f'"{quote}" - {author}\n')
    else:
        print("No quotes found.")
