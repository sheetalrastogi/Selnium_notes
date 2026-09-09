```java
import java.util.concurrent.atomic.AtomicInteger;

public class AtomicIntegerDemo {

	public static void main(String[] args) throws InterruptedException {

		CounterTask task = new CounterTask();

		Thread t1 = new Thread(task, "Thread-1");
		Thread t2 = new Thread(task, "Thread-2");
		Thread t3 = new Thread(task, "Thread-3");

		t1.start();
		t2.start();
		t3.start();

		t1.join();
		t2.join();
		t3.join();

		System.out.println("\nFinal Count = " + task.getCount());
	}
}

class CounterTask implements Runnable {

	private final AtomicInteger counter = new AtomicInteger(0);

	@Override
	public void run() {

		int newValue = counter.incrementAndGet();

		System.out.printf("%s incremented counter to %d%n", Thread.currentThread().getName(), newValue);
	}

	public int getCount() {
		return counter.get();
	}
}
```

