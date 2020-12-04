# Magento Corediff
![](https://buq.eu/screenshots/6595XfnX5wwUPzbFQGkU0GgN.png)

A forensic tool to quickly find unauthorized modifications in a Magento 1 or 2 code base. Corediff compares each line of code with a database of 1.7M legitimate code hashes and shows you the lines that have not been seen before. A bit like [@NYT_first_said](https://maxbittker.github.io/clear-pipes/).

> _"Corediff saved us countless hours"_

> _"Very useful to gauge foreign codebases"_

Corediff was created by [Sansec](https://sansec.io/?corediff), specialists in Magento security and digital forensics since 2010. Corediff analysis helped us to uncover numerous cases of server side payment skimming that would otherwise have gone undetected. 

# Usage


```
Usage:
  corediff [OPTIONS] <path>...

Application Options:
  -d, --database= Hash database path (default: download Sansec database)
  -a, --add       Add new hashes to DB, do not check
  -f, --full      Scan everything, not just core paths.
  -v, --verbose   Show what is going on

Help Options:
  -h, --help      Show this help message
```

In the following example, Corediff reports a malicious backdoor in `cron.php`:

![](https://buq.eu/screenshots/y76R3uN9CrCFN6GEji4uSPtM.png)

In default mode, Corediff will only check official Magento paths. In order to find these, you should point Corediff to the root of a Magento installation. 

Alternatively you can scan all files with the `--full` option. NB this will produce more output and requires more interpretation by a developer or forensic analyst.  

# Installation

Use our binary package:
```sh
curl https://mageintel.com/ecomscan/corediff -O
chmod 755 corediff
./corediff <magento_path> | less -SR
```
Or compile from source (requires Go 1.13+):
```sh
git clone https://github.com/sansecio/magento-corediff.git
cd magento-corediff
go run corediff.go <magento_path>
```

At the first run, `corediff` will automatically download the Sansec hash database (~26MB).

# Contributing

Adding hashes? This will create/update a database with all (new) hashes from `<path>`.

```
corediff --database=customd.db --add <path>
```

Contributions welcome! Naturally, we only accept hashes from trusted sources. [Contact us](mailto:info@sansec.io).

# About Sansec

Sansec's flagship software [eComscan](https://sansec.io) is used by ecommerce agencies, law enforcement and PCI forensic investigators. We are proud to open source many of our internal tools and hope that it will benefit our partners and customers. Malware contributions welcome.

(C) 2020 Sansec BV https://sansec.io // info@sansec.io
