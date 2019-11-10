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
