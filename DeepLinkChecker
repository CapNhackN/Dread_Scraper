#!/usr/bin/env python3
import requests
from bs4 import BeautifulSoup

#Establishing proxies to route requests over a TOR circuit
proxies= {
        'http': 'socks5h://127.0.0.1:9050',
        'https': 'socks5h://127.0.0.1:9050',
}

# Get the URL file name from the user
urls_filename = input("Enter the file name containing the URLs: ") 

# Read the URLs from the file
with open(urls_filename, "r") as file:
    urls = file.readlines()

# Keeping track of failed and successful URLs
failed_urls = []
successful_titles = []

# Loop through each URL
for url in urls:
    # Strip leading/trailing whitespace from the URL
    url = url.strip()

    # Send the web request and store the response
    html = requests.get(url, proxies=proxies, verify=False)

    # Check the status code of the response
    if html.status_code == 200:
        # If the status code is 200, parse the page source code with BeautifulSoup
        soup = BeautifulSoup(html.text, "html.parser")
        # Append the title of the page to the list of successful titles
        successful_titles.append(("Page title: ", soup.title.string))
    else:
        # If the status code is not 200, append the URL to the list of failed URLs
        failed_urls.append(url)

# Print the list of failed URLs
if failed_urls:
    print("The following URLs are unreachable:")
    for url in failed_urls:
        print(url)
else:
    print("All pages are up and responding.")

# Print the list of successful titles
if successful_titles:
    print("The following pages are up and responding:")
    for title in successful_titles:
        print(title)
else:
    print("None of the requested pages are responding.")
