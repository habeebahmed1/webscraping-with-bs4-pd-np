# Web Scraping Using BeautifulSoup, Requests, Pandas, and Numpy

In this weather I have used packages like BeautifulSoup,requests,pandas,numpy

## Import of the packages for web scraping:

![packages Image](/screen_shots/import_packages.PNG)

### Wile extracting the data from the website I used _Try and except_

## Function to extract Product Title:

![extracting_title Image](/screen_shots/extracting_title.PNG)

## Function to extract Product Price:

![extracting_price Image](/screen_shots/extracting_price.PNG)

## Function to extract Product:

![extracting_rating Image](/screen_shots/extracting_rating.PNG)

## Function to extract rating:

![extract_review Image](/screen_shots/extract_review.PNG)

## Function to extract Review:

![extracting_availibelity image](/screen_shots/extracting_availibelity.PNG)

## Extracting Data From the website:

### 1. Adding User agent

### 2. calling website URL

### 3. calling HTTP Request

### 4. creating a variable and executing the Soup Object containing all data

### 5. Fetch links as List of Tag Objects

### 6. Store the links

### 7. Loop for extracting links from Tag Objects

### 8. Loop for extracting product details from each link

for link in links_list

### 9. call function to display all necessary product information

### 10. By using Pandas DataFrame with from_dict format

### 11. Replacing empty with null value

### 12. Droping all the null values and saving the data in csv. format

### 13. call amazon_df

'''
if **name** == '**main**':

    # add your user agent
    HEADERS = ({'User-Agent':'', 'Accept-Language': 'en-US, en;q=0.5'})

    # The webpage URL
    URL = "https://www.amazon.com/s?k=playstation+4&ref=nb_sb_noss_2"

    # HTTP Request
    webpage = requests.get(URL, headers=HEADERS)

    # Soup Object containing all data
    soup = BeautifulSoup(webpage.content, "html.parser")

    # Fetch links as List of Tag Objects
    links = soup.find_all("a", attrs={'class':'a-link-normal s-no-outline'})

    # Store the links
    links_list = []

    # Loop for extracting links from Tag Objects
    for link in links:
            links_list.append(link.get('href'))

    d = {"title":[], "price":[], "rating":[], "reviews":[],"availability":[]}

    # Loop for extracting product details from each link
    for link in links_list:
        new_webpage = requests.get("https://www.amazon.com" + link, headers=HEADERS)

        new_soup = BeautifulSoup(new_webpage.content, "html.parser")

        # Function calls to display all necessary product information
        d['title'].append(get_title(new_soup))
        d['price'].append(get_price(new_soup))
        d['rating'].append(get_rating(new_soup))
        d['reviews'].append(get_review_count(new_soup))
        d['availability'].append(get_availability(new_soup))


    amazon_df = pd.DataFrame.from_dict(d)
    amazon_df['title'].replace('', np.nan, inplace=True)
    amazon_df = amazon_df.dropna(subset=['title'])
    amazon_df.to_csv("amazon_data.csv", header=True, index=False)

    amazon_df

'''

# FInal Result:

## Final Result:

![final result Image](/screen_shots/final_result.PNG)
