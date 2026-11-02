# 🚀 Bright Data 抓取浏览器

*一款完全自动化的无头浏览器解决方案，可通过 Puppeteer、Selenium 和 Playwright 进行动态网页爬虫。抓取浏览器以 GUI 形式运行在 Bright Data 基础设施上。*  

[![推广](https://github.com/bright-cn/Awesome-Web-Scraping/raw/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner%20CN.png)](https://www.bright.cn/products/scraping-browser) 

🔗 **[免费开始使用](https://www.bright.cn/products/scraping-browser)** | 📖 **[官方文档](https://docs.brightdata.com/scraping-automation/scraping-browser/introduction)**  

---

## 🔹 概述  
抓取浏览器是一款完全托管的**浏览器型抓取解决方案**，可通过**内置代理管理**、**验证码破解**和**高级网站解锁**功能，自动执行**多步骤数据采集**。它支持 **Puppeteer、Playwright 和 Selenium**，让你能够轻松实现**无限规模**的网页自动化。  

## ✅ 为什么使用抓取浏览器？  
- **无基础设施负担**：通过 API 运行和扩展浏览器会话，无需维护浏览器基础设施。  
- **内置解锁功能**：在后台自动处理 **CAPTCHA、指纹识别、重试和 JS 渲染**。  
- **多步骤导航**：自动执行点击、滚动、表单提交和悬停交互。  
- **无限扩展**：不受速率限制，可启动**数千个并发浏览器会话**。  
- **全球地理位置访问**：通过[**覆盖 195 个国家/地区的 7200 多万个住宅 IP**](https://www.bright.cn/proxy-types/residential-proxies)解锁本地化内容。  
- **无缝调试**：通过 **Chrome DevTools 集成**实时监控会话。  

---

## 🚀 快速入门  

### 安装依赖项  
确保已安装 **Node.js**、**Python** 或 **C#**，以及你偏好的网页自动化库：  

```sh
# Install Puppeteer
npm install puppeteer-core

# Install Playwright
npm install playwright

# Install Selenium
pip install selenium
```

## 🔧 使用示例

### Puppeteer 示例（JavaScript）

```js
const puppeteer = require('puppeteer-core');

const SBR_WS_ENDPOINT = 'wss://brd-customer-<YOUR-USERNAME>-zone-<YOUR-ZONE-NAME>:<YOUR-PASSWORD>@brd.superproxy.io:9222';

async function main() {
    console.log('Connecting to Scraping Browser...');
    const browser = await puppeteer.connect({ browserWSEndpoint: SBR_WS_ENDPOINT });
    try {
        const page = await browser.newPage();
        console.log('Connected! Navigating to example.com...');
        await page.goto('https://example.com');
        console.log('Scraping page content...');
        const html = await page.content();
        console.log(html);
    } finally {
        await browser.close();
    }
}

main().catch(err => console.error(err.stack || err));
```

> **💡 详细了解[使用 Puppeteer 进行网页爬虫](https://www.bright.cn/blog/how-tos/web-scraping-puppeteer)**

### Playwright 示例（Python）

```python
import asyncio
from playwright.async_api import async_playwright

SBR_WS_CDP = 'wss://brd-customer-<YOUR-USERNAME>-zone-<YOUR-ZONE-NAME>:<YOUR-PASSWORD>@brd.superproxy.io:9222'

async def run(pw):
    print('Connecting to Scraping Browser...')
    browser = await pw.chromium.connect_over_cdp(SBR_WS_CDP)
    try:
        page = await browser.new_page()
        print('Connected! Navigating to example.com...')
        await page.goto('https://example.com')
        print('Scraping page content...')
        html = await page.content()
        print(html)
    finally:
        await browser.close()

async def main():
    async with async_playwright() as playwright:
        await run(playwright)

if __name__ == '__main__':
    asyncio.run(main())
```

> **💡 详细了解[使用 Playwright 进行网页爬虫](https://www.bright.cn/blog/how-tos/playwright-web-scraping)**

### Selenium 示例（JavaScript）

```js
const { Builder, Browser } = require('selenium-webdriver');

const SBR_WEBDRIVER = 'https://brd-customer-<YOUR-USERNAME>-zone-<YOUR-ZONE-NAME>:<YOUR-PASSWORD>@brd.superproxy.io:9515';

async function main() {
    console.log('Connecting to Scraping Browser...');
    const driver = await new Builder().forBrowser(Browser.CHROME).usingServer(SBR_WEBDRIVER).build();
    try {
        console.log('Connected! Navigating to example.com...');
        await driver.get('https://example.com');
        console.log('Scraping page content...');
        const html = await driver.getPageSource();
        console.log(html);
    } finally {
        driver.quit();
    }
}

main().catch(err => console.error(err.stack || err));
```

> **💡 详细了解[使用 Selenium 进行网页爬虫](https://www.bright.cn/blog/how-tos/using-selenium-for-web-scraping)**

## 🔥 高级功能

### 使用 Chrome DevTools 进行调试

实时监控浏览器会话：

```js
const { exec } = require('child_process');

const chromeExecutable = 'google-chrome';
const openDevtools = async (page, client) => {
    const frameId = page.mainFrame()._id;
    const { url: inspectUrl } = await client.send('Page.inspect', { frameId });
    exec(`"${chromeExecutable}" "${inspectUrl}"`, error => {
        if (error) throw new Error('Unable to open devtools: ' + error);
    });
};
```

### CAPTCHA 破解

```js
const client = await page.target().createCDPSession();
const { status } = await client.send('Captcha.solve', { detectTimeout: 30000 });
```

> **🤖 详细了解我们的[验证码破解](https://github.com/bright-cn/Captcha-solver)。**

## 🔄 自动 IP 轮换与解锁  
得益于集成的[动态代理](https://www.bright.cn/solutions/rotating-proxies)，抓取浏览器会自动轮换 IP 并处理重试，从而实现无缝数据采集。 

## 💰 定价  

### 灵活套餐  
- **体验套餐（按量付费）：** $8/GB，按需付费，无需每月承诺。  
- **$499 月付计划：** $7/GB，包含 71 GB，专为寻求扩大运营的团队量身定制。  
- **$999 月付计划：** $6/GB，包含 166 GB，为具有广泛运营需求的大型团队设计。  
- **$1999 月付计划：** $5/GB，包含 399 GB，为关键业务提供高级支持和功能。  
- **企业级套餐：** 针对大规模需求提供定制定价。  

**立即注册，首次充值即可获赠相应奖励，最高可达 $500！**  

[查看定价](https://www.bright.cn/pricing/scraping-browser)  

## ❓ 常见问题  

### 抓取浏览器与标准无头浏览器有何不同？  
抓取浏览器是一款完全托管、基于 GUI 的浏览器，运行在 Bright Data 的基础设施上，甚至可以自动解锁防护最严密的网站。  

### 抓取浏览器如何应对机器人检测？  
它会自动处理指纹识别、CAPTCHA 破解和重试，并模拟真实用户行为以避免被检测。  

### 抓取浏览器是否兼容 Puppeteer、Playwright 和 Selenium？  
是的！它可以与所有主流网页自动化工具无缝集成。  

### 什么时候应该使用抓取浏览器而不是代理？  
当你需要 JavaScript 渲染、交互操作（点击、滚动）和多步骤导航时，请使用抓取浏览器。  
