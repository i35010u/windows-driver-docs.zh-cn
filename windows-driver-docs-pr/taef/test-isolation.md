---
title: 测试隔离
description: 测试隔离
ms.assetid: AC2A0060-45B9-45ff-87ED-69842F9A567D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76874e5c8a6c67f1a3ad8b1ff282bc665c86469d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374003"
---
# <a name="test-isolation"></a>测试隔离


TAEF 支持在独立进程中运行测试。 就可以控制时这些进程获取替换为 IsolationLevel 元数据和命令行选项。 这可以是对于检测意外的测试依赖项，或者降低泄漏测试的影响。

以下列表显示 IsolationLevel 元数据和命令行选项及其含义的可能的值。

<span id="None"></span><span id="none"></span><span id="NONE"></span>无  
TAEF 不会隔离任何测试。

<span id="Module"></span><span id="module"></span><span id="MODULE"></span>模块  
TAEF 将为每个测试 DLL 中使用一个单独的进程内主机。 **这是默认值。**

<span id="Assembly"></span><span id="assembly"></span><span id="ASSEMBLY"></span>程序集  
与模块相同

<span id="DLL"></span><span id="dll"></span>DLL  
与模块相同

<span id="Class"></span><span id="class"></span><span id="CLASS"></span>类  
TAEF 将使用每个测试类的一个单独的进程内主机。

<span id="Method"></span><span id="method"></span><span id="METHOD"></span>方法  
TAEF 将为每个测试使用一个单独的进程内主机。 如果在测试执行组内，同一进程内主机将用于整个执行分组。

<span id="Test"></span><span id="test"></span><span id="TEST"></span>Test  
与方法相同

使用的隔离级别的元数据值是测试级别到最接近指定的元数据。 如果还设置命令行 IsolationLevel 选项，使用的值是大多数隔离。

```cpp
BEGIN_MODULE()
    MODULE_PROPERTY(L"IsolationLevel", L"Class")
END_MODULE()

class MyTestClass1
{
    TEST_CLASS(MyTestClass1);

    BEGIN_TEST_METHOD(MyTest1)
        TEST_METHOD_PROPERTY(L"IsolationLevel", L"Method")
    END_TEST_METHOD()

    TEST_METHOD(MyTest2);
    TEST_METHOD(MyTest3);
};

class MyTestClass2
{
    TEST_CLASS(MyTestClass2);

    TEST_METHOD(MyTest1);
    TEST_METHOD(MyTest2);
};
```

在上述示例中，使用三个不同的进程内主机： 一个用于 MyTestClass1::MyTest1、 MyTestClass1 中的其他两个方法和 MyTestClass2。 如果用户要将 /IsolationLevel:Method 添加到 te.exe 的命令行，将使用五个不同的进程内主机： 一个用于每个测试。

请注意，如果一个模块中，类或测试[元数据扩展](light-weight-data-driven-testing.md)或[数据驱动](data-driven-testing.md)和是隔离，每个元数据和/或数据的扩展是隔离。 这可以防止在测试级别上通过测试的成员[执行组](execution-groups.md)。

```cpp
class MyTestClass3 :
{
    BEGIN_TEST_CLASS(MyTestClass3)
        TEST_CLASS_PROPERTY(L"Data:MyParameter1", L"{1, 2, 3}")
        TEST_CLASS_PROPERTY(L"IsolationLevel", L"Class")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTest1)
        TEST_METHOD_PROPERTY(L"Data:MyParameter2", L"{1, 2, 3}")
        TEST_METHOD_PROPERTY(L"IsolationLevel", L"Method")
        TEST_METHOD_PROPERTY(L"ExecutionGroup", L"MyExecutionGroup")
    END_TEST_METHOD()

    TEST_METHOD(MyTest2);
    TEST_METHOD(MyTest3);
};
```

在此示例中，使用六个不同的进程内主机。 每个 MyParameter1 的三个值都是独立并且 MyTest1 与 MyTest2 和 MyTest3 隔离。 MyParameter2 的三个值不是隔离的因为它们在相同的执行分组。

 

 





