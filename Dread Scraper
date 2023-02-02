#!/usr/bin/env python3
import requests
from bs4 import BeautifulSoup

#Establishing proxies to route requests over a TOR circuit
proxies= {
        'http': 'socks5h://127.0.0.1:9050',
        'https': 'socks5h://127.0.0.1:9050',
}
def web_scraper(url, terms):
    # Request the HTML content of the web page
    response = requests.get(url, proxies=proxies, verify=False)
    content = response.content

    # Use BeautifulSoup to parse the HTML content
    soup = BeautifulSoup(content, "html.parser")

    # Search for the terms within the HTML content
    results = []
    for term in terms:
        results.extend(soup.find_all(string=lambda text: term in text))
    return results

# Get the file names from the user
urls_filename = input("Enter the file name containing the URLs: ")
terms_filename = input("Enter the file name containing the search terms: ")

# Read the URLs from the file
with open(urls_filename, "r") as file:
    urls = file.readlines()

# Read the search terms from the file
with open(terms_filename, "r") as file:
    terms = file.readlines()

# Clean up the URLs and search terms by removing any leading/trailing whitespace
urls = [url.strip() for url in urls]
terms = [term.strip() for term in terms]

# Scrape each URL for the search terms
for url in urls:
    results = web_scraper(url, terms)
    if results:
        print(f"Results for URL '{url}':")
        for result in results:
            print(result)
    else:
        print(f"No results found for URL '{url}'.")
