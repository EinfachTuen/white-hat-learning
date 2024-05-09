# Aquatone 
https://github.com/michenriksen/aquatone

 is a tool for automatic and visual inspection of websites across many hosts and is convenient for quickly gaining an overview of HTTP-based attack surfaces by scanning a list of configurable ports, visiting the website with a headless Chrome browser, and taking a screenshot. This is helpful, especially when dealing with huge subdomain lists. Aquatone is not installed by default in Parrot Linux, so we will need to install via the following commands.
## Installation
```sh
sudo apt install golang chromium-driver
go install github.com/michenriksen/aquatone@latest
export PATH="$PATH":"$HOME/go/bin"
```

## Usage
```sh
aquatone --help
```
Pipe a list of subdomains into Aquatone to scan them.
```sh
cat facebook_aquatone.txt | aquatone -out ./aquatone -screenshot-timeout 1000
```
When it finishes, we will have a file called aquatone_report.html where we can see screenshots, technologies identified, server response headers, and HTML.