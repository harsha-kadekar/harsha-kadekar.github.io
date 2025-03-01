---
category: Technical
date: 2025-02-09
layout: post
title: Pointing Your Domain In Porkbun To Github Pages
updated: 2025-02-28
---

As of now, my blog is in [Github Pages](https://pages.github.com) - [harsha-kadekar.github.io](https://harsha-kadekar.github.io). The blog is developed via Jekyll and consists of only static contents. I am working on a project to update my blog, where I want to build my blogs back-end in Rust.  Once it is done, I want to host it in my own domain. As part of this, I recently bought a domain from [Porkbun](https://porkbun.com) - [harsha-kadekar.blog](https://harsha-kadekar.blog/). I thought of pointing my new domain to the current Github pages blog until migration is complete.

 [Porkbun](https://porkbun.com) had a simple one click way to add the necessary Github pages DNS configuration to my domains DNS records. I used that without reading any documentation. I tested it and saw that it was indeed going to Github but was giving 404 error. I thought I will debug it some other day and left it. Few days later, I discovered that if I try to visit my new domain, it used to take me to a random website and not to my current github pages blog. 
 
 As a first thing, I thought something is wrong in my DNS configuration. Hence, I deleted all the DNS configurations related to Github in the Porkbun's DNS management. This did not had any impact. As a next step, I started checking out the DNS configurations for each url. 
 
```shell
➜  ~ dig +short  harsha-kadekar.blog
185.199.109.153
185.199.108.153
185.199.111.153
185.199.110.153
➜  ~ dig +short  harsha-kadekar.github.io
185.199.110.153
185.199.111.153
185.199.108.153
185.199.109.153
➜  ~ dig +short AAAA harsha-kadekar.blog
2606:50c0:8001::153
2606:50c0:8000::153
2606:50c0:8003::153
2606:50c0:8002::153
➜  ~ dig +short AAAA harsha-kadekar.github.io
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

Both had the exact same A and AAAA records. This led me into thinking, probably something is wrong in the Porkbun itself and somehow they have sold my domain for not being used. I reached out to the support. They pointed out that  there could be some mistake in the Github Page configuration itself. Then, I started looking into the documents of Github. 

I discovered there is an official documentation to point our custom domain to the github pages and it involved 3 steps

### Update the DNS in Porkbun
- [Link for document reference](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

Add `A` records in the DNS management.

```
A harsha-kadekar.blog 185.199.109.153 600
A harsha-kadekar.blog 185.199.108.153 600
A harsha-kadekar.blog 185.199.111.153 600
A harsha-kadekar.blog 185.199.110.153 600
```

Add `AAAA` records in the DNS management

```
AAAA harsha-kadekar.blog 2606:50c0:8001::153 600
AAAA harsha-kadekar.blog 2606:50c0:8000::153 600
AAAA harsha-kadekar.blog 2606:50c0:8002::153 600
AAAA harsha-kadekar.blog 2606:50c0:8003::153 600
```

Add `CNAME` record

```
CNAME www.harsha-kadekar.blog harsha-kadekar.github.io 600
```

### Verify the domain in Github account 
- [Link for document reference](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)

We allow Github to verify that domain we are claiming ours is indeed belongs to ours by adding `TXT` record in the DNS management. 

The exact `TXT` record content will be provided by the Github account as part of verification process. 
- Go to settings in the github account
- Under `code, planning, and automation`, Select `Pages`
- Select `Add Domain` 
- Once you enter your domain, it will provide the `TXT` record info that needs to be added to the DNS of the domain.
- Once you have added the record, wait for some time (few hours) for DNS info to propagate. 
- After some time, click on the verify domain to validate that domain you are claiming is indeed yours.

### Add the domain in the Github Page repository
- [Link for document reference](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

Once you have verified the domain, go to the github page repository of your github pages. 
- Go to settings in the repository
- Under `code and automation`, Select `Pages`
- Under `Custom Domain`, add your custom domain address like `www.harsha-kadekar.blog`


**With these 3 steps completed, now [harsha-kadekar.blog](https://www.harsha-kadekar.blog) points to github pages  [harsha-kadekar.github.io](https://harsha-kadekar.github.io)**