from bs4 import BeautifulSoup
import requests


def check_seo_elements(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')

    title = soup.find('title').text
    meta_description = soup.find('meta',attrs={'name':'description'}) ['content']
    headers = [h.text for h in soup.findAll(['h1','h2','h3'])]

    return {
        'title': title,
        'meta_description': meta_description,
        'headers': headers
    }
url = "https://omersahin.com.tr"
seo_elements = check_seo_elements(url)
print(f"SEO Elements for '{url}':\nTitle: {seo_elements['title']}\nMeta Description:{seo_elements['meta_description']}\nHeaders:{seo_elements['headers']}")

