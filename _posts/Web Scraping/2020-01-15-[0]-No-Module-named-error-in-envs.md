---
layout: post
title: '[Error] No module named selenium in env'
tags: [selenium, web scraping]
categories: [Study/Web Scraping]
image: '/images/nomodulename_selenium.png'
---

![nomodulename_selenium](/images/nomodulename_selenium.png)

ModuleNotFoundError: No module named 'selenium' - Atom

![nomodulename_bs4](/images/nomodulename_bs4.png)

ModuleNotFoundError: No module named 'bs4' - Jupyter notebook



저 상황일 때는 아무리 `conda install pip`  등 뭘 해줘도 소용이 없었다. 난! 설치를 했는데! 왜! 넌! 없다고 말 하니? ㅠ

파이썬 버전이 2개나 깔려있으니까 (2.x / 3.x) 정확히 명시해주기로 했다. 



환경 : 맥북 카탈리나 10.15.2 - 콘다 가상환경 사용

```
python3 -m pip install BeautifulSoup4
```



**문제 해결!** 