const puppeteer = require('puppeteer');
const devices = require('puppeteer/DeviceDescriptors');
const fs = require('fs');

const DELAY = 500;

(async () => {
  let domains = [
    "domain.com",
    "domain2.com",
  ];

  const browser = await puppeteer.launch({
    headless: false,
  });
  const page = await browser.newPage();
  await page.emulate(devices['iPad landscape']);

  for (let domain of domains) {

    const url = `https://www.godaddy.com/domainsearch/find?checkAvail=1&tmskey=&domainToCheck=${domain}`;
    await page.goto(url, { waitUntil: 'networkidle2' })
    await page.waitFor('.exact-header');

    let result;

    try {
      result = await page.$eval('[data-cy="exact-header-tag"]', e => e.innerText);
      console.log(`${domain} | ${result}`);
    } catch (e) {
      console.log('an expection on page.evaluate');
    }
    await page.waitFor(DELAY);
  }

  await browser.close();
})();
