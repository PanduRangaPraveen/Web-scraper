import requests
from bs4 import BeautifulSoup

# URL of the news website (you can replace with your preferred news site)
url = "https://www.bbc.com/news"

# Send GET request
response = requests.get(url)

# Parse HTML content
soup = BeautifulSoup(response.text, "html.parser")

# Extract headlines (adjust according to site structure)
# Here, we try to find <h2> tags as headline holders
headlines = soup.find_all('h2')

# Open a file to save headlines
with open("headlines.txt", "w", encoding="utf-8") as file:
    for idx, headline in enumerate(headlines, 1):
        text = headline.get_text(strip=True)
        if text:
            file.write(f"{idx}. {text}\n")

print("Headlines scraped and saved to 'headlines.txt' successfully.")
