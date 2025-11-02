import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class SeleniumJavaCodeToAutomate {

	public static void main (String [] args) {
		
		
		WebDriver wbd =  new ChromeDriver ();
		
		wbd.manage().window().maximize();
		wbd.get("http://the-internet.herokuapp.com/nested_frames");
		System.out.println("Navigated to the URL successfully!");
		
		wbd.switchTo().frame("frame-top");
		System.out.println("Switched to the top frame!");
		
		List<WebElement> frames = wbd.findElements(By.xpath("//frame"));
		System.out.println("Numer of Frames "+ frames.size());
		if (frames.size() == 3) {
			System.out.println("verified : There are 3 frames in the top frame!");
		}
		else {
			System.out.println("Verified : Expected 3 frames but found "+ frames.size());
		}
	
		wbd.switchTo().frame("frame-left");
		String leftText = wbd.findElement(By.xpath("//body")).getText();
		if (leftText.contains("LEFT")) {
			System.out.println("Verified: Left frame text is 'LEFT'");
		}
		else {
			System.out.println("Verified : 'Expected' Left frame is not 'Left' - Failed");
		}
		
		wbd.switchTo().parentFrame();
		
		wbd.switchTo().frame("frame-middle");
		String middleText = wbd.findElement(By.xpath("//body/div")).getText();
		if (middleText.contains("MIDDLE")) {
			System.out.println("Verified: Middle frame text is 'MIDDLE'");
		} 
		else {
			System.out.println ("Verified : 'Expected' Middle frame is not 'Middle'- Failed");
		}
	
		wbd.switchTo().parentFrame();
		
		wbd.switchTo().frame("frame-right");
		String rightText = wbd.findElement(By.xpath("//body")).getText();
		if (rightText.contains("RIGHT")) {
			System.out.println("Verified: Right frame text is 'RIGHT'");
		}
		else {
			System.out.println("Verified : 'Expected' Right frame is not 'Right' - Failed");
		}
		
		wbd.switchTo().defaultContent();
		
		wbd.switchTo().frame("frame-bottom");
		String bottomText = wbd.findElement(By.xpath("//body")).getText();
		if (bottomText.contains("BOTTOM")) {
			System.out.println("Verified: Bottom frame text is 'BOTTOM'");
		}
		else {
			System.out.println("Verified : 'Expected' Bottom frame is not 'Bottom' - Failed");
		}
		
		wbd.switchTo().defaultContent();
		System.out.println("Switched back to the top frame (main content)!");

		wbd.quit();
		System.out.println ("Browser closed successfully");
	}
	
}
