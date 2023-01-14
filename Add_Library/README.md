# ROS Library

**ROS Program Tree strcuture **<br />

my_cpp_library<br />
  |<br />
  |-include<br />
  |&emsp; &emsp;   |- my_cpp_library<br />
  |&emsp; &emsp;    &emsp;&emsp;   |  <br />
  | &emsp; &emsp;    &emsp;&emsp;  |- library_header.h<br />
  |-src<br />
  |&emsp;&emsp;    |- main.cpp<br />
  |&emsp; &emsp;   |- my_cpp_library.cpp  <br />   
  |<br />
  

**CMakeLists.txt**
-----------------------------------------------------------------------------------------------------

Changes in CMakeLists.txt

-----------------------------------------------------------------------------------------------------
```
cmake_minimum_required(VERSION 3.5)
project(my_cpp_library)

if(CMAKe version)
   |
   |
   |
   |
find_package(ament_cmake REQUIRED)


include_directories(include/my_cpp_library)
set(HEADER_FILES include/my_cpp_library/library_header.h)
add_library(my_lib src/my_cpp_library.cpp ${HEADER_FILES})

add_executable(main src/main.cpp)
target_link_libraries(main PUBLIC my_lib)

#install the executable in the lib folder to be seen by setup.bash 
install(TARGETS
   main
   DESTINATION lib/${PROJECT_NAME}/
)

#export the traget in our case it is a library
ament_export_targets(my_lib HAS_LIBRARY_TARGET)

#install  include/my_cpp_library to install/ include/my_cpp_library
intsall(
   DIRECTORY include/my_cpp_library
   DESTINATION include
)


#install the target
install(
   TARGETS my_lib
   EXPORT my_lib
   LIBRARY DESTINATION lib
   ARCHIEVE DESTINATION LIB
   RUNTIME DESTINATION bin
   INCLUDES DESTINATION include
)

ament_package()
```


-----------------------------------------------------------------------------------------------------

**1. Testing**

Create a new folder tests inside my_package
```
cd ros2_ws/src/my_node
mkdir test

```
Then create main.cpp inside test folder
```
#include "gtest/gtest.h"
int main(int argc, char **argv)
{
  ::testing::InitGoogleTest(argc,argv);
  return RUN_ALL_TESTS();
}
```

Create another file in test/saving_account_test.cpp

Write the following code inside it
```
#include "gtest/gtest.h"
TEST(MyFirstTestSuite, MyFirstTest)
{
  EXPECT_TRUE(true);
}

```
  TEST is a Macro and takes 2 parameters   1. MyFirstTestSuite test suite and
  EXPECT_TRUE   is assertion and adding always true or successful. The test is going to fail
  and update CMakeLists.txt

```
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  find_package(ament_cmake_gtest REQUIRED)
  
  set(TESTFILES
     test/main.cpp
     test/saving_account_test.cpp
     )
     
   ament_add_gtest(${PROJECT_NAME}_test ${TESTFILES})
   target_link_libraries(${PROJECT_NAME}_test my_lib)
   
   install(TARGETS
      ${PROJECT_NAME}_test
      DESTINATION lib/${PROJECT_NAME}/
      )
      
      
     
     

endif()
```
-----------------------------------------------------------------------------------------------------

**2. Run Tests**

First compile 

```
cd ros2_ws
colcon build
```

Then test it for all workspace or for selected packages

```
colcon test
or
colcon test --packages-select my_cpp_library
```

To check whether the tests are successful or failed 
```
colcon test --packages-select my_cpp_library --event-handler=console_direct+

another check is
colcon test-result
```
colcon test-result show the result of previous

to check the test result of the specific package

```
colcon test-result --test-result-base build/my_cpp_library
```

-----------------------------------------------------------------------------------------------------
**3. Summarized Steps**

1. Build the package
2. Run the actual tests
3. Finally verify the test results

-----------------------------------------------------------------------------------------------------
**4.Complete Command**


```
 colcon build --packages-select my_cpp_library && colcon test --packages-select my_cpp_library && colcon test-result --test-result-base build/my_cpp_library
```

-----------------------------------------------------------------------------------------------------
**5. Few test added**

modify saving_account_test.cpp file 

```
#include "library_header.h
#include "gtest/gtest.h"

TEST(SavingsAccount, TestDeposit)
{
    SavingsAccount my_account("Holiday saving account",0);
    my_account.deposit(100);
    EXPECT_EQ(100,my_account.get_balance());
}
TEST(SavingsAccount, TestDepositAndWithdraw)
{
    SavingsAccount my_account("Holiday saving account",0);
    bool deposit_result=my_account.deposit(100.10);
    EXPECT_TRUE(deposit_result);
    ASSERT_FLOAT_EQ(100.10,my_account.get_balance());
    my_account.withdraw(50.0);
    ASSERT_FLOAT_EQ(50.10,my_account.get_balance());
}

TEST(SavingsAccount, TestExcessWithdraw)
{
    SavingsAccount my_account("Holiday saving account",555);
    bool deposit_result=my_account.deposit(100.00);
    
    EXPECT_TRUE(deposit_result);
    ASSERT_FLOAT_EQ(100.00,my_account.get_balance());
    
    bool withdraw_result=my_account.withdraw(500.00);
    EXPECT_FALSE(withdraw_result);
    ASSERT_FLOAT_EQ(100.00,my_account.get_balance());
}
TEST(SavingsAccount, TestGetName)
{
    SavingsAccount my_account("Holiday saving account",555);
    std::string name==my_account.getname();
    EXPECT_EQ("Holiday saving account",name);
}


```
-----------------------------------------------------------------------------------------------------

**6. END**






