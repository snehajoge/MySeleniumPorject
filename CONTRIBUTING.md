package MySeleniumPorject.MySeleniumPorject;



import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.Select;



public class AmazonAutomation {

	public static void main(String[] args) throws InterruptedException {
		
		
		System.setProperty("webdriver.chrome.driver", "C:\\Driver\\chromedriver.exe");
		ChromeDriver driver = new ChromeDriver();
		
		driver.manage().window().maximize();
		driver.manage().deleteAllCookies();
		
		//Navigate to Amazon
		String baseUrl="https://www.amazon.com";
		driver.get(baseUrl);
		
		String expectedTitle = "Amazon";	
		if(expectedTitle=="Amazon")
		{
			System.out.println("Correct Title");
		}
		else
	    {
			System.out.println("In-Correct Title");
		}
		
		Thread.sleep(3000);
		driver.findElement(By.xpath("//input[@id='captchacharacters']"));
		
		//Search Amazonbasics
		Thread.sleep(3000);
		WebElement searchAmazon=driver.findElement(By.xpath("//input[@id='twotabsearchtextbox']"));
		searchAmazon.sendKeys("Amazonbasics");
		searchAmazon.click();
		
		//Display Amazonbasics
		Thread.sleep(2000);
		boolean flag= searchAmazon.isDisplayed();
		System.out.println("Amazonbasics is displayed"+flag);
		
		//Select Amazon brands
		Thread.sleep(5000);
		JavascriptExecutor js = (JavascriptExecutor) driver;
		js.executeScript("window.scrollBy(0,550)", "");
		
		//Click CheclBox
		WebElement amazonBrandChkbx= driver.findElement(By.xpath("(//*[@class='a-icon a-icon-checkbox'])[5]"));
		amazonBrandChkbx.click();
		System.out.println("amazonBrandChkbx.isSelected()" + amazonBrandChkbx.isSelected());

		if(amazonBrandChkbx.isSelected()==true) 
			
		   {
			System.out.println("Option is selected");
		   }
		
		else
		    {
			System.out.println("Option is not selected");
			}
		
		//Pagination Logic
		JavascriptExecutor js1 = (JavascriptExecutor) driver;
        js1.executeScript("window.scrollBy(0,6000)","");
        //Page1
        Thread.sleep(3000);
        WebElement paginationElement = driver.findElement(By.xpath("//*[@aria-label='Go to page 3']"));
        paginationElement.click();
        
        WebElement searchProduct=driver.findElement(By.xpath("//*[text()='20W One-Port USB-C Wall Charger with Power Delivery PD for Tablets & Phones (iPhone 15/14/13/12/11/X, iPad, Samsung, and more), non-PPS, 1.81 x 1.73 x 1.09 inches, White']"));
        
        
        //Product Price
        WebElement productPrice=driver.findElement(By.xpath("//span[text()='$9.19']"));
        //productPrice.getText();
        System.out.println(productPrice);
        
        //Verify Product page display
        searchProduct.click();
        if(searchProduct.isDisplayed()==true) 
			
		   {
			System.out.println("Product is displayed");
		   }
		
		else
		    {
			System.out.println("Product is not displayed");
			}
        
        //Verify Price
        String priceText=productPrice.getText();
        double actualPrice = Double.parseDouble(priceText.replace("$", ""));
        double expectedPrice = 9.19;
		if(actualPrice==expectedPrice)
		{
			System.out.println("Correct Price"+priceText);
		}
		else
	    {
			System.out.println("In-Correct Price"+priceText);
		}
		
		//Select Random Qty
		Thread.sleep(3000);
		searchProduct.click();
		Thread.sleep(3000);
		WebElement qualtity= driver.findElement(By.xpath("//*[@id='a-autoid-0-announce']"));
		Select select = new Select(qualtity);
		select.selectByIndex(2);
		
		//Click on Add to Cart Btn
		WebElement addtoCart=driver.findElement(By.xpath("//input[@id='add-to-cart-button']"));
		addtoCart.click();
		
		//Verify Random Qty Added
		WebElement cartQuantityElement=driver.findElement(By.xpath("//*[@id='nav-cart']"));
		cartQuantityElement.click();
        int actualQuantity = Integer.parseInt(cartQuantityElement.getText());
        int expectedQuantity = 2;
        
        if (actualQuantity == expectedQuantity) {
            System.out.println("Quantity validation passed!");
        } else {
            System.out.println("Quantity validation failed!");
        }
        
        //Verify Cart Shows Count
        WebElement cartCount=driver.findElement(By.xpath("//*[@id='nav-cart-count']"));
        if(cartCount.isDisplayed()==true) 
			
		   {
			System.out.println("Product is displayed");
		   }
		
		else
		    {
			System.out.println("Product is not displayed");
			}
        
        driver.quit();
		
		

	}

}
