---
title: 使用 C + + 创作测试
description: 使用 C + + 创作测试
ms.assetid: ECADDDD6-5BD4-4c43-803F-47AE44467342
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdef10d80c0a251f870749cf8fc20698a9c2eba3
ms.sourcegitcommit: 546cc69e970e16f4e226c189da54c4fe012ae855
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84629731"
---
# <a name="authoring-tests-in-c"></a>使用 C + + 创作测试


下面的代码示例演示一个本机 c + + 文件，其中包含一个具有两个测试方法的测试类。

```cpp
1   #include "WexTestClass.h"
2
3   class SimpleTests   {
4      // Declare this class as a TestClass, and supply metadata if necessary.
5      TEST_CLASS(SimpleTests);
6
7      // Declare the tests within this class.
8      TEST_METHOD(FirstTest);
9      TEST_METHOD(SecondTest);
10  };
11
12  void SimpleTests::FirstTest()
13  {
14      VERIFY_ARE_EQUAL(1, 1);
15  }
16
17  void SimpleTests::SecondTest()
18  {
19      VERIFY_IS_TRUE(true);
20  }
```

**第1行**包括在 **% \ Program Files （x86） \windows Kits\10\Testing\Development\inc**中找到的框架**WexTestClass**所需的单个头文件。包含的标头文件还包括记录器的**Log .h**文件和用于定义验证事例的**验证 .h**文件。 稍后将讨论这些标头文件。

**第3行**定义了一个测试类**SimpleTests**。 测试类不需要从任何特殊类继承。 而且，它们的内容不需要是公共的。

**第5行**将此类定义为测试类。

**第8行和第9行**声明类**FirstTest**和**SecondTest**中的两个测试方法。 它们是在第12行到第20行上定义的。 **测试 \_ 方法**宏将所需的方法声明添加到类中。 在此标记方案中，所有测试都必须具有相同的原型。 它们必须返回**void**，并且它们必须不采用任何参数。

如果希望在类声明中以内联方式定义测试，则可以执行此操作，只要在预处理器中定义**内联 \_ 测试 \_ 方法 \_ 标记**时包含 "WexTestClass" 即可。

```cpp
1   #define INLINE_TEST_METHOD_MARKUP
2   #include "WexTestClass.h"
3
4   class InlineTests
5   {
6       TEST_CLASS(InlineTests);
7 
8       TEST_METHOD(FirstTest)
9       {
10          VERIFY_ARE_EQUAL(1, 1);
11      }
12
13      TEST_METHOD(SecondTest)
14      {
15          VERIFY_IS_TRUE(true);
16      }
17  };
```

**第10和15行**现在包含测试方法的定义。

**注意**   如果将测试类声明放在标头文件中，最好只将该头文件包含在一个 cpp 文件中。 如果将测试类声明包括到多个 CPP 文件中，则会将 extratraneous 的数据编译到测试 DLL 中。

 

## <a name="span-idadvanced_authoring_tests_in_c__spanspan-idadvanced_authoring_tests_in_c__spanspan-idadvanced_authoring_tests_in_c__spanadvanced-authoring-tests-in-c"></a><span id="Advanced_Authoring_Tests_in_C__"></span><span id="advanced_authoring_tests_in_c__"></span><span id="ADVANCED_AUTHORING_TESTS_IN_C__"></span>C + + 中的高级创作测试


下面的示例使用安装和清理方法，并声明了元数据以及测试类和测试方法声明。 此示例还包含一个具有两个测试方法的类（**MetadataAndFixturesTests**）。

```cpp
 1  #define INLINE_TEST_METHOD_MARKUP
 2  #include "WexTestClass.h"
 3
 4  BEGIN_MODULE()
 5      MODULE_PROPERTY(L"Feature", L"TAEF")
 6  END_MODULE()
 7
 8  MODULE_SETUP(ModuleSetup)
 9  {
10      return true;
11  }
12
13  MODULE_CLEANUP(ModuleCleanup)
14  {
15      return true;
16  }
17
18  class MetadataAndFixturesTests
19  {
20      BEGIN_TEST_CLASS(MetadataAndFixturesTests)
21          TEST_CLASS_PROPERTY(L"Component", L"Verify")
22      END_TEST_CLASS()
23
24      TEST_CLASS_SETUP(ClassSetup)
25      {
26          return true;
27      }
28
29      TEST_CLASS_CLEANUP(ClassCleanup)
30      {
31          return true;
32      }
33
34      TEST_METHOD_SETUP(TestSetup)
35      {
36          return true;
37      }
38
39      TEST_METHOD_CLEANUP(TestCleanup)
40      {
41          return true;
42      }
43
44      // If you use this syntax, you will have to define the test outside of the test class.
45      BEGIN_TEST_METHOD(FirstTest)
46          TEST_METHOD_PROPERTY(L"Owner", L"Contoso")
47      END_TEST_METHOD()
48
49      // You can still have metadata even if you define your test inside the test class.
50      TEST_METHOD(SecondTest)
51      {
52          BEGIN_TEST_METHOD_PROPERTIES()
53              TEST_METHOD_PROPERTY(L"Owner", L"Contoso")
54          END_TEST_METHOD_PROPERTIES()
55
56          VERIFY_IS_TRUE(true);
57      }
58  };
59
60  void MetadataAndFixturesTests::FirstTest()
61  {
62      VERIFY_ARE_EQUAL(1, 1);
63  }
```

**第4行**开始全局元数据的声明，这是一组属性，适用于此标头编译的测试二进制文件。

**第5行**声明了一个属性，该属性具有 name**功能**，值为**TAEF**。 BEGIN 之间可能有多个属性。结束 .。。macros. 类似的属性声明存在于20-24 行（类级别的元数据）、45-47 （方法级别元数据）和52-54 （内嵌定义的测试中的测试级别元数据）中。

**45 行-47 和60– 63**演示了用于添加元数据的这些测试宏还声明了测试方法。 **行 50-57**演示即使要在同一位置声明和定义测试，也仍然可以使用元数据。

**第8行**声明了一个在创建模块的任何测试类之前执行的模块安装函数。

**第13行**声明了一个模块清理函数：在所有测试和类清理方法和析构函数完成后执行的函数。 在32行上，类有类似的安装和清理方法。 这些方法在类构造函数之后、类析构函数的前面运行。

**从34到42的行**为测试方法声明了类似的函数。 测试设置和清理方法在每个测试执行之前和之后运行。

TAEF 安装和清理方法返回布尔值，并且不接受任何参数。 返回值向框架发出信号，无论是否可以继续运行特定测试单元的测试。 例如，如果类安装方法失败并返回 false，则该框架将不会运行类测试方法。

 

 





