# Puppeteer (chrome headless) Tips and Tricks

# Taking Screenshots
Taking screenshots through Puppeteer is a quite easy mission.

const puppeteer = require('puppeteer');  
async function run() {  
    let browser = await puppeteer.launch({ headless: true });   
    let page = await browser.newPage();   
    await page.setViewport({ width: 1920, height: 1080 });   
    await page.goto('https://en.wikipedia.org/wiki/Main_Page');   
    await page.screenshot({ path: './image.png', fullPage: true });   
	await page.close();   
    await browser.close();   
}   
run();  

# Generating PDF
Generating PDF through Puppeteer is very simple.

const puppeteer = require('puppeteer');  
async function run() {  
    let browser = await puppeteer.launch({ headless: true });  
    let page = await browser.newPage();  
    await page.setViewport({ width: 1920, height: 1080 });  
    await page.goto('https://en.wikipedia.org/wiki/Main_Page');  
    await page.pdf({path: 'mypdf.pdf', format: 'A4'});  
	await page.close();  
    await browser.close();  
}  
run(); 

# Faking Geolocation
const puppeteer = require('puppeteer');  
(async () => {  
  const browser = await puppeteer.launch({ devtools: true });  
  const page = await browser.newPage();  

  // Grants permission for changing geolocation  
  const context = browser.defaultBrowserContext();  
  await context.overridePermissions('https://pptr.dev', ['geolocation']);  

  await page.goto('https://pptr.dev');  
  await page.waitForSelector('title');  

  // Changes to the north pole's location  
  await page.setGeolocation({ latitude: 90, longitude: 0 });  
  await browser.close();  
})();  

# Emulating Devices
const puppeteer = require('puppeteer');  
const devices = require('puppeteer/DeviceDescriptors'); 
(async () => {  
  const browser = await puppeteer.launch({ headless: false });  
  const page = await browser.newPage();  
  await page.emulate(devices['iPhone X']);  
  await page.goto('https://pptr.dev');  
  await browser.close();  
})();  

# set Viewport
const puppeteer = require('puppeteer');  
async function run() {  
    let browser = await puppeteer.launch({ headless: false });  
    let page = await browser.newPage();  
    await page.setViewport({ width: 1920, height: 1080 });     
    await page.goto('https://www.ebay.com/');  
    await page.waitFor(10000);  
    await page.close();  
    await browser.close();  
}  
run();  

# Measuring Performance
const puppeteer = require('puppeteer');  
async function run() {  
    let browser = await puppeteer.launch({ headless: true });  
    let page = await browser.newPage();  
    await page.setViewport({ width: 1920, height: 1080 });  
    await page.goto('https://en.wikipedia.org/wiki/Main_Page');  
    const perf = await page.metrics();  
    console.log(JSON.stringify(perf));  
	await page.close();  
    await browser.close();  
}  
run();  


# code coverage using Puppeteer to Istanbul
(async () => {  
  const pti = require('puppeteer-to-istanbul')  
  const puppeteer = require('puppeteer')  
  const browser = await puppeteer.launch()  
  const page = await browser.newPage()
  // Enable both JavaScript and CSS coverage  
  await Promise.all([  
    page.coverage.startJSCoverage(),  
    page.coverage.startCSSCoverage()  
  ]);  
  // Navigate to page  
  await page.goto('https://www.google.com');  
  // Disable both JavaScript and CSS coverage  
  const [jsCoverage, cssCoverage] = await Promise.all([  
    page.coverage.stopJSCoverage(),  
    page.coverage.stopCSSCoverage(),  
  ]);  
  pti.write(jsCoverage)  
  await browser.close()  
})()  

# get accessibility
const puppeteer = require('puppeteer');  
(async () => {  
  const browser = await puppeteer.launch();  
  const page = await browser.newPage();  
  await page.goto('https://pptr.dev');  
  await page.waitForSelector('title');   
  // Captures the current state of the accessibility tree  
  const snapshot = await page.accessibility.snapshot();  
  console.info(snapshot);  
  await browser.close();  
})();  


# Request Interception
const puppeteer = require('puppeteer');  
async function run() {  
    let browser = await puppeteer.launch({ headless: false });  
    let page = await browser.newPage();  
    await page.setViewport({ width: 1920, height: 1080 });  
    await page.setRequestInterception(true);  
    page.on('request', (req) => {  
        if(req.resourceType() === 'image'){  
            req.abort();  
        }  
        else {  
            req.continue();  
        }  
    });  
    await page.goto('https://www.ebay.com/');  
    await page.waitFor(10000);  
    await page.close();  
    await browser.close();  
}  
run();  


# setUser Agent
const puppeteer = require('puppeteer');  
async function run() {  
    let browser = await puppeteer.launch({ headless: false });  
    let page = await browser.newPage();  
    await page.setViewport({ width: 1920, height: 1080 });  
	await page.setUserAgent("Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36")  
    await page.goto('https://en.wikipedia.org/wiki/Main_Page');  
    await page.waitFor(2000);  
	await page.close();  
    await browser.close();  
}  
run();  
