# cookbook
cookbook for fuff

cookbook for the Fuff tool, which can be useful for various tasks such as web fuzzing, directory discovery, and vulnerability testing. 

---

# Fuff Cookbook

Fuff (Fast, URL, Fuzzing) is a versatile tool designed for fuzzing and finding hidden directories and files on web servers. It's known for its speed and efficiency. This cookbook will cover the basics of installation, configuration, and usage with practical examples.

## Installation

Before you begin, ensure you have Go installed on your system. You can download it from [here](https://golang.org/dl/).

1. Install Fuff:

   sh
   go install github.com/ffuf/ffuf@latest
   

2. Verify the installation:

   sh
   ffuf -h
   

## Basic Usage

### 1. Simple Directory Discovery

To discover hidden directories and files on a web server, use a wordlist for fuzzing:

sh
ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt


- -u: The URL with FUZZ keyword where Fuff will substitute the wordlist items.
- -w: Path to the wordlist file.

### 2. Fuzzing with Multiple Wordlists

Fuff supports multiple wordlists for more complex fuzzing scenarios:

sh
ffuf -u http://example.com/FUZZ/FUZZ2 -w /path/to/wordlist1.txt:/path/to/wordlist2.txt -w /path/to/wordlist2.txt


### 3. Filtering and Matching

You can filter and match based on HTTP response codes, size, words, lines, or regex.

#### Filter by Status Code

sh
ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -fc 404


- -fc: Filter by response code (404 in this case).

#### Filter by Response Size

sh
ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -fs 1234


- -fs: Filter by response size (in bytes).

### 4. Recursion

To enable recursive fuzzing:

sh
ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -recursion -recursion-depth 2


- -recursion: Enable recursion.
- -recursion-depth: Set the depth of recursion.

## Advanced Usage

### 1. Fuzzing Parameters

Fuff can be used to fuzz parameters in GET or POST requests.

#### GET Request Parameter Fuzzing

sh
ffuf -u "http://example.com/page?parameter=FUZZ" -w /path/to/wordlist.txt


#### POST Request Parameter Fuzzing

sh
ffuf -u "http://example.com/page" -w /path/to/wordlist.txt -X POST -d "parameter=FUZZ"


- -X: Specify the HTTP method (POST in this case).
- -d: POST data to send.

### 2. Headers and Cookies

You can add custom headers and cookies to your requests.

sh
ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -H "X-Custom-Header: value" -b "SESSIONID=abcd1234"


- -H: Add a custom header.
- -b: Add a cookie.

### 3. Rate Limiting

To control the number of requests per second:

sh
ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -rate 100


- -rate: Set the number of requests per second.

### 4. Output

Fuff can output results in various formats for further analysis.

sh
ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -o output.json -of json


- -o: Output file.
- -of: Output file format (json, csv, or ejson).

## Practical Examples

### 1. Finding Hidden Directories

sh
ffuf -u http://example.com/FUZZ -w /usr/share/wordlists/dirb/common.txt


### 2. Fuzzing for File Extensions

sh
ffuf -u http://example.com/index.FUZZ -w /path/to/extensions.txt


### 3. Fuzzing Login Parameters

sh
ffuf -u http://example.com/login -w /path/to/wordlist.txt -X POST -d "username=admin&password=FUZZ"


### 4. Recursive Directory Discovery

sh
ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -recursion -recursion-depth 2 -fc 404


## Tips

- Use appropriate wordlists for your target. Tools like SecLists provide extensive wordlists for different purposes.
- Combine filtering options to reduce noise in results.
- Use rate limiting to avoid overwhelming the target server.

## Conclusion

Fuff is a powerful tool for web fuzzing, capable of discovering hidden files, directories, and vulnerabilities. With its speed and flexibility, it is a valuable asset for penetration testers and security researchers.



