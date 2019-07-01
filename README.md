# Selenium-JavaScript
Selenium-JavaScript Google 搜尋測試

[參考](https://itnext.io/automated-ui-testing-with-selenium-and-javascript-90bbe7ca13a3)


大致操作流程
- 抓取網址
- 爬Element(ID,ClassName).操作函式()
- 對照測資遭做是否一樣
  如原文 dalenguyen - Google Search 在台灣頁面會測試錯誤，因為台灣版本是dalenguyen - Google 搜尋

```
// test.js
// Import requirement packages
require("chromedriver");
const assert = require("assert");
const { Builder, Key, By, until } = require("selenium-webdriver");
describe("Checkout Google.com", function() {
  let driver;
  before(async function() {
    driver = await new Builder().forBrowser("chrome").build();
  });
  // Next, we will write steps for our test.
  // For the element ID, you can find it by open the browser inspect feature.
  it("Search on Google", async function() {
    // Load the page
    await driver.get("https://google.com");
    // Find the search box by id
    await driver.findElement(By.className("A8SBwf")).click();
    // Enter keywords and click enter
    await driver
      .findElement(By.className("gLFyf gsfi"))
      .sendKeys("dalenguyen", Key.RETURN);
    // Wait for the results box by id
    await driver.wait(until.elementLocated(By.id("rcnt")), 10000);
    // We will get the title value and test it
    let title = await driver.getTitle();
    assert.equal(title, "dalenguyen - Google 搜尋");
  });
  // close the browser after running tests
  after(() => driver && driver.quit());
});

```
