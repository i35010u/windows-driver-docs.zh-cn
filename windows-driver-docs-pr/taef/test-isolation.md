---
title: 测试隔离
description: 测试隔离
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18e7f0fe3dbc3a4a8c348b973947a5fda61eae69
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816467"
---
# <a name="test-isolation"></a>测试隔离


TAEF 支持在隔离的进程中运行测试。 可以控制何时将这些进程替换为 IsolationLevel metadata 和命令行选项。 这对于检测意外测试依赖项或降低泄漏测试的影响非常有用。

以下列表显示 IsolationLevel 元数据和命令行选项的可能值及其含义。

<span id="None"></span><span id="none"></span><span id="NONE"></span>内容  
TAEF 不会隔离任何测试。

<span id="Module"></span><span id="module"></span><span id="MODULE"></span>模块  
对于每个测试 DLL，TAEF 将使用单独的进程宿主。 **这是默认值。**

<span id="Assembly"></span><span id="assembly"></span><span id="ASSEMBLY"></span>件  
与模块相同

<span id="DLL"></span><span id="dll"></span>.DLL  
与模块相同

<span id="Class"></span><span id="class"></span><span id="CLASS"></span>班级  
对于每个测试类，TAEF 将使用单独的进程宿主。

<span id="Method"></span><span id="method"></span><span id="METHOD"></span>付款方式  
对于每个测试，TAEF 将使用单独的进程宿主。 如果测试在执行组中，则会将同一进程主机用于整个执行组。

<span id="Test"></span><span id="test"></span><span id="TEST"></span>考试  
与方法相同

使用的 IsolationLevel 元数据值是最接近测试级别的指定元数据。 如果同时设置了命令行 IsolationLevel 选项，则使用的值是提供最多隔离的值。

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

在上面的示例中，使用了三个不同的进程主机：一个用于 MyTestClass1：： MyTest1，另一个用于 MyTestClass1 中的其他两个方法，一个用于 MyTestClass2。 如果用户要将/IsolationLevel：方法添加到 te.exe 的命令行，则将使用5个不同的进程主机：一个用于每个测试。

请注意，如果模块、类或测试已进行 [元数据扩展](light-weight-data-driven-testing.md) 或 [数据驱动](data-driven-testing.md) ，并且它将被隔离，则每个元数据和/或数据扩展都是隔离的。 通过使测试成为 [执行组](execution-groups.md)的成员，可以对测试级别阻止此操作。

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

在此示例中，使用了六个不同的进程主机。 MyParameter1 的三个值中的每一个都是隔离的，MyTest1 独立于 MyTest2 和 MyTest3。 MyParameter2 的三个值是不隔离的，因为它们位于同一执行组中。

 

 





