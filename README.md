# S3 Bucket Scraper
A tool for scraping S3 buckets on AWS. 

Proof of concept security tool. 

Don't use it for buckets you're not allowed to access.

## How to use it

There are two programs: one is the one that scrapes S3 bucket XML, and the other will download files in keys, such as if there's a bucket for images.

This tool will not help you find S3 buckets. You need to do that yourself.

**To use this program, run bucket_scraper.py, then run key_downloader.py.**

There are 2 program files in this project:

```
bucket_scraper.py
key_downloader.py
```

Data-related files and folders:

```
bucket.txt
results.xml
key_downloads/
```

There will be a file called results.xml, which is the result of running bucket_scraper.py. If you want to run it multiple times, you will have to rename results.xml to something else, as the results will be overwritten each time.

bucket.txt is a file that contains the bucket you used to download the XML. You don't have to edit it. bucket_scraper.py will fill it out automatically.

There is also a directory called key_downloads, which is the result of downloading files specified in \<key> tags in the S3 XML.

**key_downloader.py assumes that there are files with relative paths in the \<key>s in the XML, i.e. a \<key> of image.jpg means it will be available at example.s3.amazonaws.com/image.jpg, which is the S3 bucket you specified.**

bucket_scraper.py will scrape XML of an S3 bucket.

Here's how you use it:

```
bucket_scraper.py example.s3.amazonaws.com 123
```

In the above example, example.s3.amazonaws.com is the location of the AWS S3 bucket, and 123 is the number of keys to scrape, called max-keys. If you want to get everything, you could do this:

```
scraper.py example.s3.amazonaws.com 2147483647
```

However, I've never tried that many (if you specify the signed 32-bit int max, there might be millions of S3 objects, though it will only download the XML if it exists, i.e. an S3 bucket with 1,000 items will still only have 1,000 items if you specify 100 million for max-keys), and there might be performance issues that way. The default is 1000, but you can use other amounts (usually).

I haven't tried it with massive amounts of S3 objects in a single bucket, so who knows.

key_downloader.py will download the files that are mentioned in the \<key>s in the results.xml file.

So basically, bucket_scraper.py is for downloading a list of files, and key_downloader.py downloads the files that are in the list.



