# python_test
Python Testing 100 Important Points

**100 Python test questions and answers** related to Python testing, including topics like **mocking**, **pytest**, **unittest (pyunit)**, **fixtures**, and more. These questions are categorized for better understanding.

---

### **1. General Python Testing Questions**
1. **What is unit testing?**
   - **Answer:** Unit testing is a software testing method where individual components (units) of the software are tested in isolation to ensure they work as expected.

2. **Why is testing important in Python?**
   - **Answer:** Testing ensures code reliability, catches bugs early, improves code quality, and makes refactoring safer.

3. **What is the difference between unit testing and integration testing?**
   - **Answer:** Unit testing focuses on individual components in isolation, while integration testing checks how multiple components work together.

4. **What is TDD (Test-Driven Development)?**
   - **Answer:** TDD is a development approach where tests are written before the actual code. The cycle is: Write a failing test, write code to pass the test, and refactor.

5. **What are the key components of a good test case?**
   - **Answer:** A good test case should be clear, isolated, repeatable, and test a single functionality.

---

### **2. Python `unittest` Framework**
6. **What is `unittest` in Python?**
   - **Answer:** `unittest` is a built-in Python testing framework inspired by Java's JUnit. It supports test automation, sharing of setup and shutdown code, and aggregation of tests into collections.

7. **How do you write a test case using `unittest`?**
   - **Answer:** Create a class that inherits from `unittest.TestCase` and define methods starting with `test_`.

   ```python
   import unittest

   class TestMathOperations(unittest.TestCase):
       def test_addition(self):
           self.assertEqual(1 + 1, 2)
   ```

8. **What are the key methods in `unittest.TestCase`?**
   - **Answer:** `setUp()`, `tearDown()`, `assertEqual()`, `assertTrue()`, `assertFalse()`, `assertRaises()`, etc.

9. **What is the purpose of `setUp()` and `tearDown()`?**
   - **Answer:** `setUp()` is used to prepare the test environment before each test, and `tearDown()` is used to clean up after each test.

10. **How do you run tests using `unittest`?**
    - **Answer:** Use the command `python -m unittest <test_file.py>` or add `if __name__ == "__main__": unittest.main()` to the script.

11. **What is `assertRaises` used for?**
    - **Answer:** It checks if a specific exception is raised during the execution of a code block.

    ```python
    with self.assertRaises(ValueError):
        int("invalid")
    ```

12. **How do you skip a test in `unittest`?**
    - **Answer:** Use the `@unittest.skip("reason")` decorator.

    ```python
    @unittest.skip("Not implemented yet")
    def test_subtraction(self):
        self.assertEqual(2 - 1, 1)
    ```

13. **What is a test suite in `unittest`?**
    - **Answer:** A test suite is a collection of test cases that can be executed together.

    ```python
    suite = unittest.TestLoader().loadTestsFromTestCase(TestMathOperations)
    unittest.TextTestRunner().run(suite)
    ```

14. **How do you mock a function in `unittest`?**
    - **Answer:** Use the `unittest.mock` module, specifically `patch`.

    ```python
    from unittest.mock import patch

    def my_function():
        return 42

    class TestMyFunction(unittest.TestCase):
        @patch('__main__.my_function', return_value=100)
        def test_mock(self, mock_func):
            self.assertEqual(my_function(), 100)
    ```

15. **What is the difference between `patch.object` and `patch`?**
    - **Answer:** `patch` is used to mock a function or class, while `patch.object` is used to mock a method or attribute of an object.

---

### **3. `pytest` Framework**
16. **What is `pytest`?**
    - **Answer:** `pytest` is a third-party testing framework for Python that simplifies writing and running tests. It supports fixtures, parameterized testing, and plugins.

17. **How do you install `pytest`?**
    - **Answer:** Use `pip install pytest`.

18. **How do you write a test in `pytest`?**
    - **Answer:** Write functions starting with `test_`.

    ```python
    def test_addition():
        assert 1 + 1 == 2
    ```

19. **What are fixtures in `pytest`?**
    - **Answer:** Fixtures are reusable setup and teardown functions that provide test data or resources.

    ```python
    import pytest

    @pytest.fixture
    def data():
        return [1, 2, 3]

    def test_data_length(data):
        assert len(data) == 3
    ```

20. **How do you parameterize tests in `pytest`?**
    - **Answer:** Use the `@pytest.mark.parametrize` decorator.

    ```python
    @pytest.mark.parametrize("a, b, expected", [(1, 2, 3), (4, 5, 9)])
    def test_addition(a, b, expected):
        assert a + b == expected
    ```

21. **What is the purpose of `conftest.py` in `pytest`?**
    - **Answer:** `conftest.py` is used to define fixtures and hooks that are shared across multiple test files.

22. **How do you run tests in `pytest`?**
    - **Answer:** Use the command `pytest <test_file.py>` or just `pytest` to run all tests in the directory.

23. **How do you skip a test in `pytest`?**
    - **Answer:** Use the `@pytest.mark.skip` decorator.

    ```python
    @pytest.mark.skip(reason="Not implemented yet")
    def test_subtraction():
        assert 2 - 1 == 1
    ```

24. **What is `pytest.mark` used for?**
    - **Answer:** It is used to add metadata to tests, such as `skip`, `xfail`, or custom markers.

25. **How do you mock a function in `pytest`?**
    - **Answer:** Use the `monkeypatch` fixture or `unittest.mock`.

    ```python
    def my_function():
        return 42

    def test_mock(monkeypatch):
        monkeypatch.setattr('__main__.my_function', lambda: 100)
        assert my_function() == 100
    ```

26. **What is `pytest.raises` used for?**
    - **Answer:** It checks if a specific exception is raised.

    ```python
    def test_raises():
        with pytest.raises(ValueError):
            int("invalid")
    ```

27. **How do you generate a test report in `pytest`?**
    - **Answer:** Use the `--html` or `--junitxml` options to generate reports.

    ```bash
    pytest --html=report.html
    ```

28. **What is the difference between `unittest` and `pytest`?**
    - **Answer:** `pytest` is more concise, supports fixtures, and has a rich plugin ecosystem, while `unittest` is built-in and follows an xUnit style.

29. **How do you use fixtures with parameters in `pytest`?**
    - **Answer:** Use the `params` argument in the fixture decorator.

    ```python
    @pytest.fixture(params=[1, 2, 3])
    def data(request):
        return request.param

    def test_data(data):
        assert data > 0
    ```

30. **What is `pytest-xdist`?**
    - **Answer:** It is a plugin for parallel test execution.

---

### **4. Mocking in Python**
31. **What is mocking in testing?**
    - **Answer:** Mocking is the process of replacing real objects with simulated ones to control behavior during testing.

32. **What is the `unittest.mock` module?**
    - **Answer:** It provides a `Mock` class and utilities like `patch` for creating mock objects.

33. **How do you create a mock object?**
    - **Answer:** Use the `Mock` class.

    ```python
    from unittest.mock import Mock
    mock_obj = Mock(return_value=42)
    assert mock_obj() == 42
    ```

34. **What is `patch` used for?**
    - **Answer:** It temporarily replaces an object with a mock during a test.

    ```python
    from unittest.mock import patch

    def my_function():
        return 42

    @patch('__main__.my_function', return_value=100)
    def test_mock(mock_func):
        assert my_function() == 100
    ```

35. **What is the difference between `Mock` and `MagicMock`?**
    - **Answer:** `MagicMock` is a subclass of `Mock` that automatically implements magic methods (e.g., `__len__`, `__iter__`).

36. **How do you assert that a mock was called?**
    - **Answer:** Use `assert_called()` or `assert_called_with()`.

    ```python
    mock_obj = Mock()
    mock_obj()
    mock_obj.assert_called()
    ```

37. **How do you mock a class method?**
    - **Answer:** Use `patch.object`.

    ```python
    class MyClass:
        def my_method(self):
            return 42

    with patch.object(MyClass, 'my_method', return_value=100):
        obj = MyClass()
        assert obj.my_method() == 100
    ```

38. **How do you mock a property?**
    - **Answer:** Use `PropertyMock`.

    ```python
    from unittest.mock import PropertyMock

    class MyClass:
        @property
        def my_prop(self):
            return 42

    with patch('__main__.MyClass.my_prop', new_callable=PropertyMock, return_value=100):
        obj = MyClass()
        assert obj.my_prop == 100
    ```

39. **What is `side_effect` in mocking?**
    - **Answer:** It allows you to define custom behavior for a mock, such as raising an exception or returning different values.

    ```python
    mock_obj = Mock(side_effect=[1, 2, 3])
    assert mock_obj() == 1
    assert mock_obj() == 2
    ```

40. **How do you mock a context manager?**
    - **Answer:** Use `patch` with `__enter__` and `__exit__`.

    ```python
    with patch('__main__.MyClass') as mock_obj:
        mock_obj.return_value.__enter__.return_value = 42
        with MyClass() as obj:
            assert obj == 42
    ```

---

### **5. Advanced Testing Concepts**
41. **What is dependency injection in testing?**
    - **Answer:** It is a design pattern where dependencies are passed to a component rather than created within it, making testing easier.

42. **What is the difference between stubs and mocks?**
    - **Answer:** Stubs provide predefined responses, while mocks also track interactions.

43. **What is a test double?**
    - **Answer:** It is a generic term for any object used in place of a real object during testing (e.g., mocks, stubs, fakes).

44. **What is the purpose of `coverage.py`?**
    - **Answer:** It measures code coverage to identify untested parts of the codebase.

45. **How do you measure code coverage with `pytest`?**
    - **Answer:** Use the `pytest-cov` plugin.

    ```bash
    pytest --cov=my_module
    ```

46. **What is continuous integration (CI) in testing?**
    - **Answer:** CI is a practice of automatically running tests whenever code changes are pushed to a repository.

47. **What is the difference between black-box and white-box testing?**
    - **Answer:** Black-box testing focuses on functionality without knowing internal code, while white-box testing uses internal knowledge to design tests.

48. **What is regression testing?**
    - **Answer:** It ensures that new changes do not break existing functionality.

49. **What is the purpose of `tox` in testing?**
    - **Answer:** `tox` is a tool for testing Python code against multiple environments and dependencies.

50. **What is the difference between `pytest` and `nose2`?**
    - **Answer:** `nose2` is another testing framework, but `pytest` is more popular and feature-rich.

---

### **6. Practical Testing Scenarios**
51. **How do you test a function that reads a file?**
    - **Answer:** Use mocking to simulate file reading.

    ```python
    from unittest.mock import mock_open, patch

    def read_file(path):
        with open(path, 'r') as f:
            return f.read()

    @patch('builtins.open', mock_open(read_data="file content"))
    def test_read_file():
        assert read_file('dummy_path') == "file content"
    ```

52. **How do you test a function that makes an HTTP request?**
    - **Answer:** Use `requests-mock` or `unittest.mock`.

    ```python
    import requests
    from unittest.mock import patch

    def fetch_data(url):
        return requests.get(url).json()

    @patch('requests.get')
    def test_fetch_data(mock_get):
        mock_get.return_value.json.return_value = {'key': 'value'}
        assert fetch_data('http://example.com') == {'key': 'value'}
    ```

53. **How do you test a function that uses a database?**
    - **Answer:** Use an in-memory database or mocking.

    ```python
    from unittest.mock import MagicMock

    def query_db(db, query):
        return db.execute(query).fetchall()

    def test_query_db():
        mock_db = MagicMock()
        mock_db.execute.return_value.fetchall.return_value = [(1, 'Alice')]
        assert query_db(mock_db, 'SELECT * FROM users') == [(1, 'Alice')]
    ```

54. **How do you test a function with side effects?**
    - **Answer:** Use mocking to isolate the side effects.

    ```python
    from unittest.mock import patch

    def send_email(email):
        # Simulate sending email
        return True

    @patch('__main__.send_email', return_value=True)
    def test_send_email(mock_send):
        assert send_email('test@example.com') is True
    ```

55. **How do you test a function that depends on time?**
    - **Answer:** Use `freezegun` or mocking.

    ```python
    from datetime import datetime
    from freezegun import freeze_time

    def get_current_time():
        return datetime.now()

    @freeze_time("2023-10-01")
    def test_get_current_time():
        assert get_current_time() == datetime(2023, 10, 1)
    ```

---

### **7. Miscellaneous Questions**
56. **What is the purpose of `assert` in Python?**
    - **Answer:** It is used to check if a condition is true. If not, it raises an `AssertionError`.

57. **What is the difference between `assertEqual` and `assertAlmostEqual`?**
    - **Answer:** `assertEqual` checks for exact equality, while `assertAlmostEqual` allows for a small difference (useful for floating-point numbers).

58. **What is the purpose of `assertRaisesRegex`?**
    - **Answer:** It checks if an exception is raised and if the error message matches a regex pattern.

59. **How do you test private methods in Python?**
    - **Answer:** Use `unittest` or `pytest` to test private methods, but it's generally discouraged. Instead, test public methods that use private methods.

60. **What is the purpose of `pytest.mark.xfail`?**
    - **Answer:** It marks a test as expected to fail.

    ```python
    @pytest.mark.xfail
    def test_failing():
        assert 1 == 2
    ```

61. **What is the purpose of `pytest.mark.skipif`?**
    - **Answer:** It skips a test if a condition is true.

    ```python
    import sys

    @pytest.mark.skipif(sys.version_info < (3, 8), reason="Requires Python 3.8+")
    def test_new_feature():
        assert True
    ```

62. **What is the purpose of `pytest.mark.usefixtures`?**
    - **Answer:** It applies a fixture to a test without passing it as an argument.

    ```python
    @pytest.fixture
    def data():
        return [1, 2, 3]

    @pytest.mark.usefixtures('data')
    def test_data_length():
        assert len(data) == 3
    ```

63. **What is the purpose of `pytest.mark.parametrize`?**
    - **Answer:** It allows you to run the same test with different inputs.

    ```python
    @pytest.mark.parametrize("a, b, expected", [(1, 2, 3), (4, 5, 9)])
    def test_addition(a, b, expected):
        assert a + b == expected
    ```

64. **What is the purpose of `pytest.mark.timeout`?**
    - **Answer:** It sets a timeout for a test.

    ```python
    @pytest.mark.timeout(5)
    def test_slow_function():
        time.sleep(10)
    ```

65. **What is the purpose of `pytest.mark.filterwarnings`?**
    - **Answer:** It filters warnings during test execution.

    ```python
    @pytest.mark.filterwarnings("ignore:deprecated")
    def test_warning():
        warnings.warn("deprecated", DeprecationWarning)
    ```

---

### **8. Performance Testing**
66. **What is performance testing?**
    - **Answer:** It checks how a system performs under a particular workload, focusing on speed, responsiveness, and stability.


67. **How do you measure the execution time of a function in Python?**
    - **Answer:** Use the `time` module or `timeit` module.

    ```python
    import time

    start_time = time.time()
    my_function()
    end_time = time.time()
    print(f"Execution time: {end_time - start_time} seconds")
    ```

68. **What is the purpose of `timeit` in Python?**
    - **Answer:** `timeit` is a module used to measure the execution time of small code snippets with high precision.

    ```python
    import timeit

    execution_time = timeit.timeit('my_function()', globals=globals(), number=1000)
    print(f"Average execution time: {execution_time / 1000} seconds")
    ```

69. **How do you profile Python code for performance?**
    - **Answer:** Use the `cProfile` module.

    ```python
    import cProfile

    cProfile.run('my_function()')
    ```

70. **What is the difference between `cProfile` and `profile`?**
    - **Answer:** `cProfile` is implemented in C and is faster, while `profile` is implemented in Python and provides more detailed output.

71. **How do you test for memory leaks in Python?**
    - **Answer:** Use tools like `tracemalloc` or `objgraph`.

    ```python
    import tracemalloc

    tracemalloc.start()
    my_function()
    snapshot = tracemalloc.take_snapshot()
    for stat in snapshot.statistics('lineno'):
        print(stat)
    ```

72. **What is the purpose of `pytest-benchmark`?**
    - **Answer:** It is a plugin for benchmarking and performance testing in `pytest`.

    ```python
    def test_benchmark(benchmark):
        benchmark(my_function)
    ```

73. **How do you simulate high load in performance testing?**
    - **Answer:** Use tools like `locust`, `JMeter`, or `multiprocessing` to simulate multiple users or processes.

74. **What is the difference between load testing and stress testing?**
    - **Answer:** Load testing checks performance under expected load, while stress testing checks performance under extreme conditions.

75. **How do you test the scalability of a Python application?**
    - **Answer:** Gradually increase the workload (e.g., number of users, data size) and measure performance metrics like response time and resource usage.

---

### **9. Integration Testing**
76. **What is integration testing?**
    - **Answer:** Integration testing checks how multiple components or modules work together.

77. **How do you write integration tests in Python?**
    - **Answer:** Use frameworks like `pytest` or `unittest` to test interactions between components.

78. **What is the difference between unit testing and integration testing?**
    - **Answer:** Unit testing focuses on individual components, while integration testing focuses on interactions between components.

79. **How do you mock external APIs in integration testing?**
    - **Answer:** Use tools like `requests-mock` or `unittest.mock`.

    ```python
    import requests
    from requests_mock import Mocker

    def test_external_api():
        with Mocker() as m:
            m.get('https://api.example.com', json={'key': 'value'})
            response = requests.get('https://api.example.com')
            assert response.json() == {'key': 'value'}
    ```

80. **What is the purpose of `pytest-django`?**
    - **Answer:** It is a plugin for testing Django applications with `pytest`.

81. **How do you test database interactions in Django?**
    - **Answer:** Use Django's `TestCase` or `pytest-django` to test database queries and transactions.

82. **What is the purpose of `factory_boy` in testing?**
    - **Answer:** It is a library for creating test data fixtures in a clean and reusable way.

83. **How do you test a REST API in Python?**
    - **Answer:** Use libraries like `requests` and `pytest` to send HTTP requests and validate responses.

    ```python
    import requests

    def test_api():
        response = requests.get('https://api.example.com/endpoint')
        assert response.status_code == 200
        assert response.json() == {'key': 'value'}
    ```

84. **What is the purpose of `pytest-flask`?**
    - **Answer:** It is a plugin for testing Flask applications with `pytest`.

85. **How do you test asynchronous code in Python?**
    - **Answer:** Use `pytest-asyncio` or `unittest.IsolatedAsyncioTestCase`.

    ```python
    import pytest
    import asyncio

    async def async_function():
        await asyncio.sleep(1)
        return 42

    @pytest.mark.asyncio
    async def test_async_function():
        result = await async_function()
        assert result == 42
    ```

---

### **10. Behavior-Driven Development (BDD)**
86. **What is BDD?**
    - **Answer:** BDD is a development approach that focuses on defining behavior using natural language and automating tests based on those definitions.

87. **What is `behave` in Python?**
    - **Answer:** `behave` is a BDD framework for Python that uses Gherkin syntax.

88. **What is Gherkin syntax?**
    - **Answer:** Gherkin is a human-readable language for defining test scenarios using keywords like `Given`, `When`, and `Then`.

    ```gherkin
    Feature: Login functionality
      Scenario: Successful login
        Given I am on the login page
        When I enter valid credentials
        Then I should be redirected to the dashboard
    ```

89. **How do you write a step definition in `behave`?**
    - **Answer:** Define Python functions that map to Gherkin steps.

    ```python
    from behave import given, when, then

    @given('I am on the login page')
    def step_impl(context):
        context.browser.visit('/login')

    @when('I enter valid credentials')
    def step_impl(context):
        context.browser.fill('username', 'user')
        context.browser.fill('password', 'pass')
        context.browser.find_by_css('button[type="submit"]').click()

    @then('I should be redirected to the dashboard')
    def step_impl(context):
        assert context.browser.is_text_present('Dashboard')
    ```

90. **What is the purpose of `pytest-bdd`?**
    - **Answer:** It is a plugin for implementing BDD with `pytest`.

91. **How do you parameterize scenarios in `pytest-bdd`?**
    - **Answer:** Use the `@pytest.mark.parametrize` decorator.

    ```python
    @pytest.mark.parametrize('username, password', [('user1', 'pass1'), ('user2', 'pass2')])
    def test_login(username, password):
        assert login(username, password) is True
    ```

92. **What is the difference between `behave` and `pytest-bdd`?**
    - **Answer:** `behave` is a standalone BDD framework, while `pytest-bdd` integrates BDD with `pytest`.

93. **How do you generate reports in `behave`?**
    - **Answer:** Use the `--format` option to generate reports in formats like JSON or HTML.

    ```bash
    behave --format json -o report.json
    ```

94. **What is the purpose of `allure-behave`?**
    - **Answer:** It is a plugin for generating Allure reports with `behave`.

95. **How do you test edge cases in BDD?**
    - **Answer:** Define scenarios that cover unusual or extreme inputs.

    ```gherkin
    Scenario: Login with invalid credentials
      Given I am on the login page
      When I enter invalid credentials
      Then I should see an error message
    ```

---

### **11. Security Testing**
96. **What is security testing?**
    - **Answer:** Security testing checks for vulnerabilities in the application, such as SQL injection, XSS, or insecure APIs.

97. **How do you test for SQL injection in Python?**
    - **Answer:** Use tools like `sqlmap` or write tests that simulate malicious inputs.

98. **What is the purpose of `bandit` in Python?**
    - **Answer:** `bandit` is a tool for identifying common security issues in Python code.

99. **How do you test for XSS vulnerabilities?**
    - **Answer:** Simulate malicious inputs and check if they are rendered as HTML.

100. **What is the purpose of `pytest-selenium`?**
    - **Answer:** It is a plugin for testing web applications using Selenium with `pytest`.


