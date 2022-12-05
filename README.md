# IdrisDemo
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
//import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.edge.EdgeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.WebDriverWait;
import java.io.IOException;
import java.time.Duration;
import java.util.concurrent.TimeUnit;
import org.openqa.selenium.By;
import org.openqa.selenium.Keys;



public class SeleniumTest {
		public static void main(String[] args) {

		//WebDriver driver = new ChromeDriver();

		WebDriver driver = new EdgeDriver();
		

		String baseUrl = "https://www.saucedemo.com/";
		String UserName = "standard_user";
		String Password = "secret_sauce";
		String expectedTitle  = "THANK YOU FOR YOUR ORDER";
		String actualTitle = "";

		// Open Browser and maximize window
		driver.get(baseUrl);
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));

		//Login, add items to cart and checkout
		driver.findElement(By.name("user-name")).sendKeys(UserName);
		driver.findElement(By.name("password")).sendKeys(Password);
		driver.findElement(By.name("login-button")).click();
		driver.findElement(By.xpath("(//button[@id='add-to-cart-sauce-labs-backpack'])[1]")).click();
		driver.findElement(By.xpath("//button[@id='add-to-cart-sauce-labs-bike-light']")).click();
		driver.findElement(By.xpath("//a[@class='shopping_cart_link']")).click();
		driver.findElement(By.name("checkout")).click();
		driver.findElement(By.name("firstName")).sendKeys("Name");
		driver.findElement(By.name("lastName")).sendKeys("Surname");
		driver.findElement(By.name("postalCode")).sendKeys("2000");
		driver.findElement(By.name("continue")).click();
		driver.findElement(By.name("finish")).click();
		actualTitle = driver.findElement(By.xpath("//h2[normalize-space()='THANK YOU FOR YOUR ORDER']")).getText();

		//Validate
        if (actualTitle.contentEquals(expectedTitle)){
            System.out.println("Test Passed!");
        } else {
            System.out.println("Test Failed");
        }

	
		driver.quit();

		
	}
}

