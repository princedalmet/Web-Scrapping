
# Web Scraper with Python

In this article, I’m going to create a web scraper with Python that pulls all the stories from Google News by extracting all the tags from the HTML of Google News.

Google News uses tags to create links to the various websites that make up the site. So in addition to some additional data, you’ll collect all the URLs of the articles that Google News displays. I will use the BeautifulSoup module to analyze the articles from Google News.

Parsing means taking a format like HTML and using a programming language to give it structure. For example, transforming data into an object. Now, to start this task of creating a web scraper with Python, you need to install a module named BeautifulSoup. It can be easily installed using the pip command; 

pip install beautifulsoup4.





## Web Scraper with Python
Python has a built-in module, named urllib, for working with URLs. Add the following code to a new Python file:

import urllib.request
from bs4 import BeautifulSoup


class Scraper:

    def __init__(self, site):

        self.site = site

The __init__ method uses a website to extract as a parameter. Later you will pass “https://news.google.com/” as a parameter. The Scraper class has a method called scrape that you will call whenever you want to retrieve data from the site you passed.

Add the following code to your scrape method:

def scrape(self):

        r = urllib.request.urlopen(self.site)

        html = r.read()

The urlopen () function sends a request to a website and returns a Response object in which its HTML code is stored, along with additional data. The response of the function. read () returns the HTML of the Response object. All the HTML for the website is in the html variable.

You are now ready to analyze the HTML. Add a new line of code in the scrape function which creates a BeautifulSoup object, and pass the html variable and the “html.parser” string as a parameter:

def scrape(self):

        r = urllib.request.urlopen(self.site)

        html = r.read()

        parser = "html.parser"

        sp = BeautifulSoup(html,parser)

The BeautifulSoup object does all the hard work and parses the HTML. You can now add code to the scrape function that calls the find_all method on the BeautifulSoup object.

Pass “a” as the parameter and the method will return all the URLs the website is linked to in the HTML code you downloaded:

def scrape(self):

        r = urllib.request.urlopen(self.site)

        html = r.read()

        parser = "html.parser"

        sp = BeautifulSoup(html,parser)

        for tag in sp.find_all("a"):

            url = tag.get("href")

            if url is None:

                continue

            if "articles" in url:

                print("\n" + url)

The find_all method returns an iterable containing the tag objects found. Each time around the for loop, the variable receives the value of a new Tag object. Each Tag object has many different instance variables, but you just want the value of the href instance variable, which contains each URL.

You can get it by calling the get method and passing “href” as a parameter. Finally, you verify that the URL variable contains data; that it contains the string “articles” (you don’t want to print internal links); and if so, you print it. Here is the full web scraper:

./articles/CAIiEDQkcZshPCX6jqGgfKrpBcQqFwgEKg4IACoGCAoww7k_MMevCDDIrqcH?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEDQkcZshPCX6jqGgfKrpBcQqFwgEKg4IACoGCAoww7k_MMevCDDIrqcH?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEDQkcZshPCX6jqGgfKrpBcQqFwgEKg4IACoGCAoww7k_MMevCDDIrqcH?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEJq9is3xlFpkTJ-hffNwQSoqGQgEKhAIACoHCAowzrL9CjDC7vQCMOXc1gU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEJq9is3xlFpkTJ-hffNwQSoqGQgEKhAIACoHCAowzrL9CjDC7vQCMOXc1gU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiELC3rSlFZvpgsvCmlDdHaPkqGQgEKhAIACoHCAowot7cCjD8xM4BMMfHhgI?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiELC3rSlFZvpgsvCmlDdHaPkqGQgEKhAIACoHCAowot7cCjD8xM4BMMfHhgI?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMie2h0dHBzOi8vZWNvbm9taWN0aW1lcy5pbmRpYXRpbWVzLmNvbS9vcGluaW9uL2V0LWVkaXRvcmlhbC91cy1iYW5zLXJ1c3NpYW4tb2lsLWluZGlhLW5lZWRzLXRvLXBpdm90L2FydGljbGVzaG93LzkwMDg1NDU5LmNtc9IBdmh0dHBzOi8vbS5lY29ub21pY3RpbWVzLmNvbS9vcGluaW9uL2V0LWVkaXRvcmlhbC91cy1iYW5zLXJ1c3NpYW4tb2lsLWluZGlhLW5lZWRzLXRvLXBpdm90L2FtcF9hcnRpY2xlc2hvdy85MDA4NTQ1OS5jbXM?hl=en-IN&gl=IN&ceid=IN%3Aen        

./articles/CBMie2h0dHBzOi8vZWNvbm9taWN0aW1lcy5pbmRpYXRpbWVzLmNvbS9vcGluaW9uL2V0LWVkaXRvcmlhbC91cy1iYW5zLXJ1c3NpYW4tb2lsLWluZGlhLW5lZWRzLXRvLXBpdm90L2FydGljbGVzaG93LzkwMDg1NDU5LmNtc9IBdmh0dHBzOi8vbS5lY29ub21pY3RpbWVzLmNvbS9vcGluaW9uL2V0LWVkaXRvcmlhbC91cy1iYW5zLXJ1c3NpYW4tb2lsLWluZGlhLW5lZWRzLXRvLXBpdm90L2FtcF9hcnRpY2xlc2hvdy85MDA4NTQ1OS5jbXM?hl=en-IN&gl=IN&ceid=IN%3Aen        

./articles/CAIiEFOYbt-aulx8kzCSwXtlv_8qFwgEKg8IACoHCAowjuuKAzCWrzwwt4QY?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEFOYbt-aulx8kzCSwXtlv_8qFwgEKg8IACoHCAowjuuKAzCWrzwwt4QY?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEKSH5Np8Pp8VXRTIDYOJUPEqGAgEKg8IACoHCAow3rvTBDD89X4w8YzmBQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEKSH5Np8Pp8VXRTIDYOJUPEqGAgEKg8IACoHCAow3rvTBDD89X4w8YzmBQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEKSH5Np8Pp8VXRTIDYOJUPEqGAgEKg8IACoHCAow3rvTBDD89X4w8YzmBQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CCAiC0VycjZxallhd3BRmAEB?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CCAiC0VycjZxallhd3BRmAEB?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEAeRUMYkVQCNe8Ifd9uhbkkqGQgEKhAIACoHCAowzrL9CjDC7vQCMK2y1gU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEAeRUMYkVQCNe8Ifd9uhbkkqGQgEKhAIACoHCAowzrL9CjDC7vQCMK2y1gU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMivgFodHRwczovL3RpbWVzb2ZpbmRpYS5pbmRpYXRpbWVzLmNvbS9jaXR5L2x1Y2tub3cvdXAtbmV3cy1saXZlLXVwZGF0ZXMtYXNzZW1ibHktZWxlY3Rpb25zLWV4aXQtcG9sbHMteW9naS1hZGl0eWFuYXRoLWFraGlsZXNoLXlhZGF2LW1heWF3YXRpLXByaXlhbmthLWdhbmRoaS1tYXJjaC05LTIwMjIvbGl2ZWJsb2cvOTAwODQzNjUuY21z0gHCAWh0dHBzOi8vdGltZXNvZmluZGlhLmluZGlhdGltZXMuY29tL2NpdHkvbHVja25vdy91cC1uZXdzLWxpdmUtdXBkYXRlcy1hc3NlbWJseS1lbGVjdGlvbnMtZXhpdC1wb2xscy15b2dpLWFkaXR5YW5hdGgtYWtoaWxlc2gteWFkYXYtbWF5YXdhdGktcHJpeWFua2EtZ2FuZGhpLW1hcmNoLTktMjAyMi9hbXBfbGl2ZWJsb2cvOTAwODQzNjUuY21z?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMivgFodHRwczovL3RpbWVzb2ZpbmRpYS5pbmRpYXRpbWVzLmNvbS9jaXR5L2x1Y2tub3cvdXAtbmV3cy1saXZlLXVwZGF0ZXMtYXNzZW1ibHktZWxlY3Rpb25zLWV4aXQtcG9sbHMteW9naS1hZGl0eWFuYXRoLWFraGlsZXNoLXlhZGF2LW1heWF3YXRpLXByaXlhbmthLWdhbmRoaS1tYXJjaC05LTIwMjIvbGl2ZWJsb2cvOTAwODQzNjUuY21z0gHCAWh0dHBzOi8vdGltZXNvZmluZGlhLmluZGlhdGltZXMuY29tL2NpdHkvbHVja25vdy91cC1uZXdzLWxpdmUtdXBkYXRlcy1hc3NlbWJseS1lbGVjdGlvbnMtZXhpdC1wb2xscy15b2dpLWFkaXR5YW5hdGgtYWtoaWxlc2gteWFkYXYtbWF5YXdhdGktcHJpeWFua2EtZ2FuZGhpLW1hcmNoLTktMjAyMi9hbXBfbGl2ZWJsb2cvOTAwODQzNjUuY21z?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEMIxOMBf05sKtaMdUHwuEggqGQgEKhAIACoHCAowr6n9CjCr4PQCMN791QM?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEMIxOMBf05sKtaMdUHwuEggqGQgEKhAIACoHCAowr6n9CjCr4PQCMN791QM?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEAp05NEvBxZqgd7zmmTGge4qGQgEKhAIACoHCAowj8n_CjDIrfkCMPGi6AU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEAp05NEvBxZqgd7zmmTGge4qGQgEKhAIACoHCAowj8n_CjDIrfkCMPGi6AU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEAp05NEvBxZqgd7zmmTGge4qGQgEKhAIACoHCAowj8n_CjDIrfkCMPGi6AU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEOqDJ_-E506eeJ9x7xGXOr8qGQgEKhAIACoHCAowzrL9CjDC7vQCMOXc1gU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEOqDJ_-E506eeJ9x7xGXOr8qGQgEKhAIACoHCAowzrL9CjDC7vQCMOXc1gU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMicGh0dHBzOi8vaW5kaWFuZXhwcmVzcy5jb20vYXJ0aWNsZS93b3JsZC9wb2xhbmQtcmVhZHktdG8tcGxhY2UtYWxsLWl0cy1taWctMjktamV0cy1hdC10aGUtZGlzcG9zYWwtb2YtdXMtNzgwNzg4OS_SAXVodHRwczovL2luZGlhbmV4cHJlc3MuY29tL2FydGljbGUvd29ybGQvcG9sYW5kLXJlYWR5LXRvLXBsYWNlLWFsbC1pdHMtbWlnLTI5LWpldHMtYXQtdGhlLWRpc3Bvc2FsLW9mLXVzLTc4MDc4ODkvbGl0ZS8?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMicGh0dHBzOi8vaW5kaWFuZXhwcmVzcy5jb20vYXJ0aWNsZS93b3JsZC9wb2xhbmQtcmVhZHktdG8tcGxhY2UtYWxsLWl0cy1taWctMjktamV0cy1hdC10aGUtZGlzcG9zYWwtb2YtdXMtNzgwNzg4OS_SAXVodHRwczovL2luZGlhbmV4cHJlc3MuY29tL2FydGljbGUvd29ybGQvcG9sYW5kLXJlYWR5LXRvLXBsYWNlLWFsbC1pdHMtbWlnLTI5LWpldHMtYXQtdGhlLWRpc3Bvc2FsLW9mLXVzLTc4MDc4ODkvbGl0ZS8?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMicWh0dHBzOi8vd3d3Lm5kdHYuY29tL3dvcmxkLW5ld3MvcmVhZHktdG8tZGVwbG95LW1pZy0yOS1maWdodGVyLWpldHMtdG8tdXMtYWlyLWJhc2UtaW4tZ2VybWFueS1zYXlzLXBvbGFuZC0yODExODM40gF3aHR0cHM6Ly93d3cubmR0di5jb20vd29ybGQtbmV3cy9yZWFkeS10by1kZXBsb3ktbWlnLTI5LWZpZ2h0ZXItamV0cy10by11cy1haXItYmFzZS1pbi1nZXJtYW55LXNheXMtcG9sYW5kLTI4MTE4MzgvYW1wLzE?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMicWh0dHBzOi8vd3d3Lm5kdHYuY29tL3dvcmxkLW5ld3MvcmVhZHktdG8tZGVwbG95LW1pZy0yOS1maWdodGVyLWpldHMtdG8tdXMtYWlyLWJhc2UtaW4tZ2VybWFueS1zYXlzLXBvbGFuZC0yODExODM40gF3aHR0cHM6Ly93d3cubmR0di5jb20vd29ybGQtbmV3cy9yZWFkeS10by1kZXBsb3ktbWlnLTI5LWZpZ2h0ZXItamV0cy10by11cy1haXItYmFzZS1pbi1nZXJtYW55LXNheXMtcG9sYW5kLTI4MTE4MzgvYW1wLzE?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEISpWcVabN1sDtuHJ77VE5gqGQgEKhAIACoHCAow2pqGCzD954MDMPTVigY?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEISpWcVabN1sDtuHJ77VE5gqGQgEKhAIACoHCAow2pqGCzD954MDMPTVigY?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEJwpPaJ_VH_7XYLU_rHwwT0qGQgEKhAIACoHCAow5qqNCzD4q58DMPbXpwY?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEJwpPaJ_VH_7XYLU_rHwwT0qGQgEKhAIACoHCAow5qqNCzD4q58DMPbXpwY?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEJwpPaJ_VH_7XYLU_rHwwT0qGQgEKhAIACoHCAow5qqNCzD4q58DMPbXpwY?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMiemh0dHBzOi8vZWNvbm9taWN0aW1lcy5pbmRpYXRpbWVzLmNvbS9uZXdzL2luZGlhL3VrcmFpbmUtY3Jpc2lzLXRvLWhlbHAtY3V0LXdoZWF0LXByb2N1cmVtZW50LWJpbGwvYXJ0aWNsZXNob3cvOTAwODY0MTQuY21z0gF1aHR0cHM6Ly9tLmVjb25vbWljdGltZXMuY29tL25ld3MvaW5kaWEvdWtyYWluZS1jcmlzaXMtdG8taGVscC1jdXQtd2hlYXQtcHJvY3VyZW1lbnQtYmlsbC9hbXBfYXJ0aWNsZXNob3cvOTAwODY0MTQuY21z?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMiemh0dHBzOi8vZWNvbm9taWN0aW1lcy5pbmRpYXRpbWVzLmNvbS9uZXdzL2luZGlhL3VrcmFpbmUtY3Jpc2lzLXRvLWhlbHAtY3V0LXdoZWF0LXByb2N1cmVtZW50LWJpbGwvYXJ0aWNsZXNob3cvOTAwODY0MTQuY21z0gF1aHR0cHM6Ly9tLmVjb25vbWljdGltZXMuY29tL25ld3MvaW5kaWEvdWtyYWluZS1jcmlzaXMtdG8taGVscC1jdXQtd2hlYXQtcHJvY3VyZW1lbnQtYmlsbC9hbXBfYXJ0aWNsZXNob3cvOTAwODY0MTQuY21z?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEJ7GNq8z-RTbwkLBlaK-p-MqGAgEKg8IACoHCAow3rvTBDD89X4w8ZXmBQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEJ7GNq8z-RTbwkLBlaK-p-MqGAgEKg8IACoHCAow3rvTBDD89X4w8ZXmBQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEJgmpZSzzpQjnoJh1L-DxrIqGAgEKg8IACoHCAowjtSUCjC30XQw_qe5AQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEJgmpZSzzpQjnoJh1L-DxrIqGAgEKg8IACoHCAowjtSUCjC30XQw_qe5AQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMiggFodHRwczovL3d3dy5tb25leWNvbnRyb2wuY29tL25ld3Mvb3Bpbmlvbi9jaGFydC1vZi10aGUtZGF5LXVrcmFpbmUtcnVzc2lhLXNpdHVhdGlvbi1zZW5kcy1nbG9iYWwtZm9vZC1wcmljZXMtc2t5d2FyZHMtODIwMDkxMS5odG1s0gGGAWh0dHBzOi8vd3d3Lm1vbmV5Y29udHJvbC5jb20vbmV3cy9vcGluaW9uL2NoYXJ0LW9mLXRoZS1kYXktdWtyYWluZS1ydXNzaWEtc2l0dWF0aW9uLXNlbmRzLWdsb2JhbC1mb29kLXByaWNlcy1za3l3YXJkcy04MjAwOTExLmh0bWwvYW1w?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMiggFodHRwczovL3d3dy5tb25leWNvbnRyb2wuY29tL25ld3Mvb3Bpbmlvbi9jaGFydC1vZi10aGUtZGF5LXVrcmFpbmUtcnVzc2lhLXNpdHVhdGlvbi1zZW5kcy1nbG9iYWwtZm9vZC1wcmljZXMtc2t5d2FyZHMtODIwMDkxMS5odG1s0gGGAWh0dHBzOi8vd3d3Lm1vbmV5Y29udHJvbC5jb20vbmV3cy9vcGluaW9uL2NoYXJ0LW9mLXRoZS1kYXktdWtyYWluZS1ydXNzaWEtc2l0dWF0aW9uLXNlbmRzLWdsb2JhbC1mb29kLXByaWNlcy1za3l3YXJkcy04MjAwOTExLmh0bWwvYW1w?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEFOgmIfVPVJpnzKj6K-QFPMqGQgEKhAIACoHCAowzrL9CjDC7vQCMJmD1wU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEFOgmIfVPVJpnzKj6K-QFPMqGQgEKhAIACoHCAowzrL9CjDC7vQCMJmD1wU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEFOgmIfVPVJpnzKj6K-QFPMqGQgEKhAIACoHCAowzrL9CjDC7vQCMJmD1wU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMibmh0dHBzOi8vd3d3LnRoZWhpbmR1LmNvbS9uZXdzL25hdGlvbmFsL3plbGVuc2t5LXNheXMtaGUtc3Bva2UtdG8tbW9kaS10by1wdXQtYW4tZW5kLXRvLXdhci9hcnRpY2xlNjUyMDQyMzUuZWNl0gFzaHR0cHM6Ly93d3cudGhlaGluZHUuY29tL25ld3MvbmF0aW9uYWwvemVsZW5za3ktc2F5cy1oZS1zcG9rZS10by1tb2RpLXRvLXB1dC1hbi1lbmQtdG8td2FyL2FydGljbGU2NTIwNDIzNS5lY2UvYW1wLw?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMibmh0dHBzOi8vd3d3LnRoZWhpbmR1LmNvbS9uZXdzL25hdGlvbmFsL3plbGVuc2t5LXNheXMtaGUtc3Bva2UtdG8tbW9kaS10by1wdXQtYW4tZW5kLXRvLXdhci9hcnRpY2xlNjUyMDQyMzUuZWNl0gFzaHR0cHM6Ly93d3cudGhlaGluZHUuY29tL25ld3MvbmF0aW9uYWwvemVsZW5za3ktc2F5cy1oZS1zcG9rZS10by1tb2RpLXRvLXB1dC1hbi1lbmQtdG8td2FyL2FydGljbGU2NTIwNDIzNS5lY2UvYW1wLw?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiECBEGTzn1o3ubjKXa1g56asqFwgEKg4IACoGCAoww7k_MMevCDDIrqcH?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiECBEGTzn1o3ubjKXa1g56asqFwgEKg4IACoGCAoww7k_MMevCDDIrqcH?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CCAiC2ZTWlo2NG11TVRjmAEB?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CCAiC2ZTWlo2NG11TVRjmAEB?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMicWh0dHBzOi8vd3d3Lm5ld3MxOC5jb20vbmV3cy9pbmRpYS9wbS1tb2RpLXNwZWFrcy10by1kdXRjaC1jb3VudGVycGFydC1tYXJrLXJ1dHRlLW92ZXItdWtyYWluZS1jcmlzaXMtNDg1MjU1OS5odG1s0gF1aHR0cHM6Ly93d3cubmV3czE4LmNvbS9hbXAvbmV3cy9pbmRpYS9wbS1tb2RpLXNwZWFrcy10by1kdXRjaC1jb3VudGVycGFydC1tYXJrLXJ1dHRlLW92ZXItdWtyYWluZS1jcmlzaXMtNDg1MjU1OS5odG1s?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMicWh0dHBzOi8vd3d3Lm5ld3MxOC5jb20vbmV3cy9pbmRpYS9wbS1tb2RpLXNwZWFrcy10by1kdXRjaC1jb3VudGVycGFydC1tYXJrLXJ1dHRlLW92ZXItdWtyYWluZS1jcmlzaXMtNDg1MjU1OS5odG1s0gF1aHR0cHM6Ly93d3cubmV3czE4LmNvbS9hbXAvbmV3cy9pbmRpYS9wbS1tb2RpLXNwZWFrcy10by1kdXRjaC1jb3VudGVycGFydC1tYXJrLXJ1dHRlLW92ZXItdWtyYWluZS1jcmlzaXMtNDg1MjU1OS5odG1s?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEFEIMDUjcY1-QrjULOSXy_cqGAgEKg8IACoHCAow3rvTBDD89X4w8YzmBQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEFEIMDUjcY1-QrjULOSXy_cqGAgEKg8IACoHCAow3rvTBDD89X4w8YzmBQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEFEIMDUjcY1-QrjULOSXy_cqGAgEKg8IACoHCAow3rvTBDD89X4w8YzmBQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CCAiC0xZZ0xTdTFaSzQ4mAEB?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CCAiC0xZZ0xTdTFaSzQ4mAEB?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEHLoMGig_7O8qEgxDFY2AX8qGQgEKhAIACoHCAowzrL9CjDC7vQCMK2y1gU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEHLoMGig_7O8qEgxDFY2AX8qGQgEKhAIACoHCAowzrL9CjDC7vQCMK2y1gU?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEHYvPJEVHbGYGpkLMcgx2_kqFwgEKg4IACoGCAoww7k_MMevCDDIrqcH?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CAIiEHYvPJEVHbGYGpkLMcgx2_kqFwgEKg4IACoGCAoww7k_MMevCDDIrqcH?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMijQFodHRwczovL3d3dy50ZWxlZ3JhcGhpbmRpYS5jb20vbXkta29sa2F0YS9uZXdzL2luZGlhbi1lbWJhc3N5LWFib3J0cy1ldmFjdWF0aW9uLWZyb20tc3VteS1zdHVkZW50cy10YWtlbi1iYWNrLXRvLWhvc3RlbHMtZnJvbS1idXMvY2lkLzE4NTUwMDnSAZEBaHR0cHM6Ly93d3cudGVsZWdyYXBoaW5kaWEuY29tL2FtcC9teS1rb2xrYXRhL25ld3MvaW5kaWFuLWVtYmFzc3ktYWJvcnRzLWV2YWN1YXRpb24tZnJvbS1zdW15LXN0dWRlbnRzLXRha2VuLWJhY2stdG8taG9zdGVscy1mcm9tLWJ1cy9jaWQvMTg1NTAwOQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMijQFodHRwczovL3d3dy50ZWxlZ3JhcGhpbmRpYS5jb20vbXkta29sa2F0YS9uZXdzL2luZGlhbi1lbWJhc3N5LWFib3J0cy1ldmFjdWF0aW9uLWZyb20tc3VteS1zdHVkZW50cy10YWtlbi1iYWNrLXRvLWhvc3RlbHMtZnJvbS1idXMvY2lkLzE4NTUwMDnSAZEBaHR0cHM6Ly93d3cudGVsZWdyYXBoaW5kaWEuY29tL2FtcC9teS1rb2xrYXRhL25ld3MvaW5kaWFuLWVtYmFzc3ktYWJvcnRzLWV2YWN1YXRpb24tZnJvbS1zdW15LXN0dWRlbnRzLXRha2VuLWJhY2stdG8taG9zdGVscy1mcm9tLWJ1cy9jaWQvMTg1NTAwOQ?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMic2h0dHBzOi8vd3d3LmFsdG5ld3MuaW4vdGhlLWhpbmR1LWpvdXJuYWxpc3QtZmFsc2VseS1hdHRhY2tlZC1mb3ItcmVwb3J0aW5nLXRuLWdvdnQtcGFpZC1mb3ItZXZhY3VhdGlvbi1vZi1zdHVkZW50cy_SAQA?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMic2h0dHBzOi8vd3d3LmFsdG5ld3MuaW4vdGhlLWhpbmR1LWpvdXJuYWxpc3QtZmFsc2VseS1hdHRhY2tlZC1mb3ItcmVwb3J0aW5nLXRuLWdvdnQtcGFpZC1mb3ItZXZhY3VhdGlvbi1vZi1zdHVkZW50cy_SAQA?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMiiAFodHRwczovL3d3dy5ib29tbGl2ZS5pbi9mYWN0LWNoZWNrL3J1c3NpYS11a3JhaW5lLWludmFzaW9uLXdhci1jb25mbGljdC1pbmRpYW4tbWVkaWEtc3RhZ2VkLXJlcG9ydGluZy1mYWtlLWRlYXRoLWJvZHktYmFncy1uZXdzLTI0LTE3MDIy0gEA?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMiiAFodHRwczovL3d3dy5ib29tbGl2ZS5pbi9mYWN0LWNoZWNrL3J1c3NpYS11a3JhaW5lLWludmFzaW9uLXdhci1jb25mbGljdC1pbmRpYW4tbWVkaWEtc3RhZ2VkLXJlcG9ydGluZy1mYWtlLWRlYXRoLWJvZHktYmFncy1uZXdzLTI0LTE3MDIy0gEA?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMijwFodHRwczovL3d3dy5pbmRpYXRvZGF5LmluL2ZhY3QtY2hlY2svc3RvcnkvZmFjdC1jaGVjay1vbGQtdW5yZWxhdGVkLWltYWdlcy1wYXNzZWQtb2ZmLWFzLXJlY2VudC1waG90b3MtZnJvbS13YXItdG9ybi11a3JhaW5lLTE5MjEzOTItMjAyMi0wMy0wNtIBAA?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMijwFodHRwczovL3d3dy5pbmRpYXRvZGF5LmluL2ZhY3QtY2hlY2svc3RvcnkvZmFjdC1jaGVjay1vbGQtdW5yZWxhdGVkLWltYWdlcy1wYXNzZWQtb2ZmLWFzLXJlY2VudC1waG90b3MtZnJvbS13YXItdG9ybi11a3JhaW5lLTE5MjEzOTItMjAyMi0wMy0wNtIBAA?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMihAFodHRwczovL2ZhY3RseS5pbi9uby1tb2RpLXppbmRhYmFkLXNsb2dhbnMtd2VyZS1ub3QtcmFpc2VkLWluLXRoZS1wYWtpc3Rhbi1wYXJsaWFtZW50LXByYWlzaW5nLWluZGlhcy1ldmFjdWF0aW9uLWVmZm9ydHMtaW4tdWtyYWluZS_SAQA?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMihAFodHRwczovL2ZhY3RseS5pbi9uby1tb2RpLXppbmRhYmFkLXNsb2dhbnMtd2VyZS1ub3QtcmFpc2VkLWluLXRoZS1wYWtpc3Rhbi1wYXJsaWFtZW50LXByYWlzaW5nLWluZGlhcy1ldmFjdWF0aW9uLWVmZm9ydHMtaW4tdWtyYWluZS_SAQA?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMiYWh0dHBzOi8vd3d3LmFsdG5ld3MuaW4vZGlkLWluZGlhbi1zdHVkZW50cy1pbi11a3JhaW5lLXBheS1uby1oZWVkLXRvLWVub3VnaC13YXJuaW5ncy1ieS10aGUtZ292dC_SAQA?hl=en-IN&gl=IN&ceid=IN%3Aen

./articles/CBMiYWh0dHBzOi8vd3d3LmFsdG5ld3MuaW4vZGlkLWluZGlhbi1zdHVkZW50cy1pbi11a3JhaW5lLXBheS1uby1oZWVkLXRvLWVub3VnaC13YXJuaW5ncy1ieS10aGUtZ292dC_SAQA?hl=en-IN&gl=IN&ceid=IN%3Aen