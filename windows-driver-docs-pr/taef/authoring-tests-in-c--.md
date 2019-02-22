---
title: C + + 中创作测试
description: C + + 中创作测试
ms.assetid: ECADDDD6-5BD4-4c43-803F-47AE44467342
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09279d214edab919394e26c6e4e1f541d3876dd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519094"
---
# <a name="authoring-tests-in-c"></a>C + + 中创作测试


下面的代码示例显示了包含单个测试类具有两个测试方法的本机 c + + 文件。

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

**第 1 行**包含所需的框架，单个标头文件**WexTestClass.h**。 该包含的头文件还包括**Log.h**记录器的文件和**Verify.h**用于定义验证的情况下的文件。 稍后将讨论这些标头文件。

**第 3 行**定义一个测试类， **SimpleTests**。 测试类不必继承任何特殊的类。 此外，其内容不需要是公共的。

**第 5 行**为测试类中定义此类。

**行 8 和 9**声明两个测试方法在类中的**FirstTest**并**SecondTest**。 在定义行至第 20 12。 **测试\_方法**宏将所需的方法声明添加到类。 在此标记方案中，所有测试必须都具有相同的原型。 它们必须返回**void**，且它们必须接受任何参数。

如果你想要定义在类声明中的测试内联，则可以执行的只要包括"WexTestClass.h"时**内联\_测试\_方法\_标记**中定义预处理器。

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

**第 10 和 15 行**现在包含测试方法的定义。

**请注意**  如果标头文件中将测试类声明中，最好仅到一个 cpp 文件中包括该标头文件。 Extratraneous 数据编译到测试 DLL 中包括到多个 CPP 文件结果的测试类声明。

 

## <a name="span-idadvancedauthoringtestsincspanspan-idadvancedauthoringtestsincspanspan-idadvancedauthoringtestsincspanadvanced-authoring-tests-in-c"></a><span id="Advanced_Authoring_Tests_in_C__"></span><span id="advanced_authoring_tests_in_c__"></span><span id="ADVANCED_AUTHORING_TESTS_IN_C__"></span>C + + 中的高级创作测试


下面的示例使用的设置和清理方法，并声明元数据以及在测试类和测试方法声明。 此示例还包含一个类 (**MetadataAndFixturesTests**) 具有两个测试方法。

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

**第 4 行**开始全局元数据，一组应用于此标头将编译的测试二进制文件的属性的声明。

**第 5 行**声明具有名称属性**功能**和值**TAEF**。 可能有多个开始之间的单个属性...日期和结束...宏。 行 20 到 24 个 （类级别的元数据）、 45-47 （方法级别元数据） 和 52 54 （测试级别元数据中定义的测试内联） 上存在类似的属性声明。

**第 45 47 和 60 – 63 行**演示这些测试宏用于添加元数据还将测试方法声明。 **行 50-57**演示你仍可以包含元数据，即使你想要声明和定义测试在相同的位置。

**第 8 行**声明模块的安装程序函数的任何模块的测试类创建之前执行的函数。

**第 13 行**声明模块的清理函数-测试和类清理方法和析构函数完成所有执行的函数。 有类似的设置和行 24 类清理方法但 32。 这些方法分别运行之后的类构造函数和类析构函数之前。

**行通过 42 34**声明类似函数的测试方法。 测试设置和清理方法运行之前和之后执行每个测试。

TAEF 设置和清理方法返回布尔值，并不接受任何参数。 返回值向发出信号，该框架是否可以继续运行某些测试单元测试。 例如，如果类安装方法失败，并返回 false，该框架不会运行类测试方法。

 

 





