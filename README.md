# Puppeteer Tips and Tricks

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

