# JUnit - JUnit is a unit testing framework for the Java programming language.

### assertEquals, assertFalse, assertTrue

```js
public class StringHelperTest {
	StringHelper helper = new StringHelper();

	// Test method should be always public void

	@Test
	public void testTruncateAInFirst2Positions_AinFirst2Positions() {
		// expected, actual value
		assertEquals("CD", helper.truncateAInFirst2Positions("AACD"));
	}

	@Test
	public void testTruncateAInFirst2Positions_AinFirstPosition() {
		assertEquals("CD", helper.truncateAInFirst2Positions("ACD"));
	}

	@Test
	public void testAreFirstAndLastTwoCharactersTheSame_BasicNegativeScenerio() {
		// assertEquals(false, helper.areFirstAndLastTwoCharactersTheSame("ABCD"));
		// assertFalse(helper.areFirstAndLastTwoCharactersTheSame("AABCAA"));

		assertFalse("Condition failed", helper.areFirstAndLastTwoCharactersTheSame("ABCAA"));
	}
	
	@Test
	public void testAreFirstAndLastTwoCharactersTheSame_BasicPositiveScenerio() {
		assertTrue("Condition passed", helper.areFirstAndLastTwoCharactersTheSame("AABCAA"));
	}
}
```

### Before & After

```js
public class QuickBeforeAfterTest {

	@Before
	public void setup() {
		System.out.println("Before Setup");
	}

	@Test
	public void test1() {
		System.out.println("Test1 Executed");
	}

	@Test
	public void test2() {
		System.out.println("Test2 Executed");
	}

	@After
	public void teardown() {
		System.out.println("After Test");
	}
}
```

### Before & After Class

```js
public class BeforeAndAfterClassTest {

	@BeforeClass
	public static void setup() {
		System.out.println("Before Setup");
	}

	@Test
	public void test1() {
		System.out.println("Test1 Executed");
	}

	@Test
	public void test2() {
		System.out.println("Test2 Executed");
	}

	@AfterClass
	public static void teardown() {
		System.out.println("After Test");
	}
}
```

### Array

```js
public class TestArray {

	@Test
	public void test() {
		int[] numbers = { 5, 2, 3, 1, 4 };
		int[] expected = { 1, 2, 3, 4, 5 };

		Arrays.sort(numbers);

		assertArrayEquals(expected, numbers);
	}

}
```

## Exception & Performance

```js
public class TestExceptionAndPerformance {

	@Test(expected = NullPointerException.class)
	public void test() {
		int[] numbers = null;
		Arrays.sort(numbers);
	}

	@Test(timeout = 1000)
	public void testSortPerformance() {
		int[] array = { 1, 2, 3 };
		for (int i = 0; i < 1000000000; i++) {
			array[0] = i;
			Arrays.sort(array);
		}
	}
}
```

### Parameterized Test

```js
@RunWith(Parameterized.class)
public class ParameterizedTest {
	StringHelper helper = new StringHelper();

	private String input;
	private String expected;

	public ParameterizedTest(String input, String expected) {
		super();
		this.input = input;
		this.expected = expected;
	}

	@Parameters
	public static Collection<String[]> testConditions() {
		String expectedOutput[][] = { { "AACD", "CD" }, 
									  { "ACD", "CD" } };

		return Arrays.asList(expectedOutput);
	}

	@Test
	public void testTruncateAInFirst2Positions_AinFirst2Positions() {
		// expected, actual value
		assertEquals(expected, helper.truncateAInFirst2Positions(input));
	}
}
```

### Test Suites

```js
@RunWith(Suite.class)
@SuiteClasses({ BeforeAndAfterClassTest.class, ParameterizedTest.class })
public class AllTests {

}
```
