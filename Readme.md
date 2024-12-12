# Wikipedia Scraper

This project is a simple web scraping script written in Python that retrieves the main content of a Wikipedia page for a given person's name. The script uses the `requests` and `BeautifulSoup` libraries to fetch and parse the Wikipedia page.

## Features
- Fetches the Wikipedia page for a specified person.
- Extracts and displays the main heading (`<h1>` tag) and the main content (`<p>` tags).
- Cleans up references (e.g., `[1]`, `[2]`, etc.) from the extracted text.

## How to Use

### Prerequisites
- Python 3.x
- Required Python libraries:
  - `requests`
  - `BeautifulSoup` (from `bs4`)

You can install the required libraries using pip:
```bash
pip install requests beautifulsoup4
```

### Running the Script
1. Clone the repository or download the script.
2. Run the script in your terminal or any Python IDE.
3. Enter the name of the person whose Wikipedia page you want to scrape when prompted.

Example:
```bash
python wikipedia_scraper.py
```
Input:
```
Enter the Person Name: Albert_Einstein
```
Output:
```
Heading: Albert Einstein
Content: Albert Einstein was a theoretical physicist who ...
```

## Code Explanation
```python
import requests
from bs4 import BeautifulSoup

title = input("Enter the Person Name :")
link = 'https://en.wikipedia.org/wiki/' + title
res = requests.get(link)
soup = BeautifulSoup(res.text, 'html.parser')

# Extracting heading
heading = soup.find('h1').text

# Extracting and cleaning the main content
para = ''
for p in soup.find_all('p'):
    para += p.text
para = para.strip()
for i in range(500):
    para = para.replace('[' + str(i) + ']', '')

print("Heading:", heading)
print("Content:", para)
```

## Future Enhancements
- Add error handling for invalid inputs or network issues.
- Include a feature to save the extracted content into a text file.
- Expand the script to scrape other sections of the Wikipedia page, such as tables or infoboxes.

## License
This project is licensed under the MIT License. Feel free to use, modify, and distribute it.

---

Happy Coding! :snake:
