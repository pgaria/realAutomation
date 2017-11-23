---
title: "Integrate TestRail with Automated TestCases in Java+TestNG"
date: 2017-11-23T14:15:09+01:00
draft: false
---

#### What is TestRail?
TestRail (http://www.gurock.com/testrail/) is a modern and very nice tool for the Test Case Management by Quality Assurance and Development Team.
TestManagement tools are very helpful for managing the test cases and TestRail is pack with very useful features like web-based application, Rest API integration etc.

![Image Title](/img/testRail/TestRailReport.png)

#### Why to use TestManagement Tool with Automation?
While making Regression or any kind of Test Automation suit there is a need of maintaining Use cases and maintain the repository which anyone can access and see what use cases are been automated and what is left. It is very helpful for the continues Integration Pipeline that we can generate and see the reports in one place for Automated Test results.

![Image Title](/img/testRail/TestCaseResult.png)

There is a need for Integrating Test Management Tool like TestRail with the Java and TestNG based Automated Test Framework to mark every test run results in the common web-based platform.
In this blog, I am going to use TestRail as Test Management tool and will explain the steps to integrate your framework using Rest API's.

#### How to integrate Automated Test with TestRail?
I am explaining the steps to write your logic in Java and you can also follow the steps to make integration work for your framework

STEP 1: First create one new Annotation class 
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface UseAsTestRailId
{
int testRailId() default 0;
String[] tags() default "";
}
```
STEP 2: Use the above annotation in TestNg Class File with Other Test.

Every @Test here is mapped with the Use case In TestRail So we got the TestRail Unique Id for every Test.
```java
@Test
@UseAsTestRailId(testRailId=<TestRail Id for this Usecase>)
public void yourTestNumberSomething()
{
  // Do your testing Steps here which are mapped to testRail Case.
}
```
STEP 3: You can Use TestNG for Every Test So that you can execute the Test Rail API after the test Execution.
```java
@Listeners(com.gurock.testrail.Listener.class)
public class TestIngClass {
    // All the Test Will be here ...
}
```
STEP 4: You need to Call the test Rail from Listener Class. Like I am Calling the API in the on Test Success Method.
```java
public void onTestSuccess(ITestResult result) {
String TestID=null;
IClass obj = result.getTestClass();
Class newobj = obj.getRealClass();
Method testMethod = newobj.getMethod(result.getName());
if (testMethod.isAnnotationPresent(UseAsTestRailId.class)) 
{
UseAsTestRailId useAsTestName = testMethod.getAnnotation(UseAsTestRailId.class);
// Get the TestCase ID for Test Rail
TestID = Integer.toString(useAsTestName.testRailId());
System.out.println("Test Rail ID = " + TestID);
}
// Now You can call the Test Rail Post API call to update the Result in Test Rail Based on the Test Run Id and TestCase ID.

JSONObject r = (JSONObject) client.sendPost("add_result_for_case/TestCaseID/TestRunID", data);
}
```
#### Final Result and Reporting
Now Integrating TestRail UseCases Id with Automated Test, We will have the test Run result history for the particular UseCases.

![Image Title](/img/testRail/TestRailUseCaseReport.png)  

You can change and improve the code and Logic based on your requirements and send me feedback about your experience with the integration.

Thanks for reading!
