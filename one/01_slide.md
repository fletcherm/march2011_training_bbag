!SLIDE 
Knowlogy Weeklong TDD Training
==============================

!SLIDE center
![K](k.jpg)

!SLIDE bullets
Ceedling
========
* Unity
* CMock
* CException

!SLIDE code smaller
Unity
=====
    @@@ C
    #include "unity.h"

    void setUp(void) {}
    void tearDown(void) {}

    void test_NumberValidator_IsNumber_DoesNotAcceptBlankString(void) {}

    void test_NumberValidator_IsNumber_AcceptsZero(void) {}

!SLIDE bullets incremental
Assertions
==========
* `TEST_ASSERT`
* `TEST_ASSERT_FALSE`
* `TEST_ASSERT_EQUAL`

!SLIDE smaller

    @@@ C
    void test_NumberValidator_IsNumber_AcceptsNegativeIntegers(void)
    {
      TEST_ASSERT(NumberValidator_IsNumber("-5"));
      TEST_ASSERT(NumberValidator_IsNumber("-5555"));
      TEST_ASSERT(NumberValidator_IsNumber("-93899393"));
    }

!SLIDE smaller

    @@@ C
    void test_NumberValidator_IsNumber_DoesNotAcceptNonNumbers(void)
    {
      TEST_ASSERT_FALSE(NumberValidator_IsNumber("-"));
      TEST_ASSERT_FALSE(NumberValidator_IsNumber(" -a"));
      TEST_ASSERT_FALSE(NumberValidator_IsNumber("abc"));
      TEST_ASSERT_FALSE(NumberValidator_IsNumber("a"));
      TEST_ASSERT_FALSE(NumberValidator_IsNumber("100%"));
    }

!SLIDE bullets
CMock
=====
* follows convention to generate mock files from a header

!SLIDE small
CMock
=====
    @@@ C
    #include "ApplicationPresenter.h"
    #include "mock_ApplicationModel.h"
    #include "mock_ApplicationView.h"

    void test_ApplicationPresenter_ShowsErrorWhenBadArgs() {
      ApplicationView_GetDivisor_ExpectAndReturn("21");
      ApplicationView_GetDividend_ExpectAndReturn("0");
      ApplicationModel_ValidateArguments
                      _ExpectAndReturn("21", "0", FALSE);
      ApplicationView_ShowError_Expect();

      ApplicationPresenter_CalculateClickedCallback();
    }

!SLIDE bullets incremental
Linkage
=======
* tests are linked against real source, mock dependence
* source is linked against real dependence

!SLIDE
insert image here

!SLIDE bullets
CException
==========
* exception handling implemented with setjmp and longjmp

!SLIDE bullets
Ceedling
========
* compile source
* generate mocks
* compile tests
* run tests

!SLIDE bullets incremental
Last week
=========
* 1/2 Monday - intro to TDD and tools
* 1/2 Monday - small sample project walkthrough
* Tuesday, Wednesday, Thursday - socket project w/ cucumbers
* 1/2 Friday - more Agile ideas (iterations, burndowns, etc)

!SLIDE bullets incremental
Sample project
==============
* client - server apps
* put and get (pid, name) tuples for an id
* cucumbers for both client and server
* use cucumbers to guide features, use ceedling tools to guide development

!SLIDE code small
    Feature: Ping command
    As a client
    I want to ping the server and see a response

    Scenario: Pinging the server
    Given the server is online
    When I ping the server
    Then the client should receive a positive response
    And the exit status should be 0

!SLIDE code small
    Feature: Put and get commands
    As a server
    ...

    Scenario: Putting and getting multiple pairs
    Given the server is online
    When I put the pid "1" with the name "init" for id "abc"
    And I put the pid "99" with the name "ps" for id "abc"
    And I put the pid "187" with the name "ruby" for id "abc"

    When I get the pairs for id "abc"
    Then the pid "1" with the name "init" should be returned
    And the pid "99" with the name "ps" should be returned
    And the pid "187" with the name "ruby" should be returned


!SLIDE code small
    Scenario: Putting and getting different ids
    Given the server is online
    When I put the pid "1" with the name "init" for id "123"
    And I put the pid "99" with the name "ps" for id "abc"

    When I get the pairs for id "123"
    Then the pid "1" with the name "init" should be returned

    When I get the pairs for id "abc"
    Then the pid "99" with the name "ps" should be returned

!SLIDE bullets incremental
Successes
=========
* All groups got client working
* One - two groups got server working
* Github repository made pushing fixes and changes easy
* Git branches for server, client helped overcome limitations and keep things separated

!SLIDE bullets incremental
* Smart group that enjoyed the course and working together
* Gave good feedback on how to improve course and material
* Very involved and interested in Agile PM discussion
* Hinted another group is interested in training as well
* ~$157 effective rate

!SLIDE bullets incremental
Improvements
============
* document client - server protocol (rspec?)
* better intro to straight unit testing, then mocks
* better intro to system tests (ok, what do I run???)
* go through example of making usage pass?
