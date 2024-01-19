# Top 17M website host URL

This repository contains the most popular 17M website host URLs according to the Google CRUX dataset.

I have exported this dataset using the BigQuery interface and downloaded - this dataset is freely available and free to use by anyone directly from Google as well. It here for your convenience.

The CSV file contains the top 17M domains and their popularity as order of magnitude starting with 1000, sorted by popularity ascending with the url sorted secondarily.

The format is "url,popularity" - example:

```bash
http(s)://domain.com,1000
```

## Working with the dataset

Due to GitHub limitations, the file is compressed with 7z, so start by decompressing it:

```bash
7z x crux-2023-12-top17m.7z
```

Then you can use [ripgrep](https://github.com/BurntSushi/ripgrep) to get the information you need

### Strip the order of magnitude and just keep the URL

```bash
rg "^(.*),[0-9]+$" -r '$2' crux-2023-12-top17m.csv > top17m-urls.txt
```

### Keep just the host name

```bash
rg "^http(s)?://(.*),[0-9]+$" -r '$2' crux-2023-12-top17m.csv > top17m-hosts.txt
```

### Keep just the domain name

```bash
rg "^http(s)?://.*?(?<domain>[^.]*[.]?.{6}),[0-9]+$" -r '$domain' crux-2023-12-top17m.csv > top17-domains.txt
```

### Limit to less than 17M entries

You can extract the top 1000 urls/hosts/domains using the following command:

```bash
head -n 1000 crux-2023-12-top17m.csv > top-1000.csv
```

Useful intervals for these cutoffs are 1000, 5000, 10000, 50000, 100000, 500000, 1000000, 5000000, 10000000, 50000000 (last is only from 10-17M)

### Mass download stuff

You can feed host names into [turbograb](https://github.com/lkarlslund/turbograb) if you quickly want to download the primary page from each site

## Happy hunting

Feedback is welcome -> Mastodon [@lkarlslund](https://infosec.exchange/@lkarlslund) / Twitter [@lkarlslund](https://twitter.com/lkarlslund) / LinkedIn [Lars Karlslund](https://www.linkedin.com/in/lkarlslund/)
