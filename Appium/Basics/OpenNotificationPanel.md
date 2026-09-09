```java
	public static void openNotificationPanel(AppiumDriver driver) {

		Dimension size = driver.manage().window().getSize();

		int x = size.width / 2;
		int startY = 5;
		int endY = size.height / 2;

		PointerInput finger = new PointerInput(PointerInput.Kind.TOUCH, "finger");

		Sequence sequence = new Sequence(finger, 0);

		sequence.addAction(finger.createPointerMove(Duration.ZERO, PointerInput.Origin.viewport(), x, startY));

		sequence.addAction(finger.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));

		sequence.addAction(finger.createPointerMove(Duration.ofMillis(800), PointerInput.Origin.viewport(), x, endY));

		sequence.addAction(finger.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));

		driver.perform(List.of(sequence));
	}

```
