---
title: 并行程序
description: 并行程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c74371122db97e04ffec849a8ec5ab963a81f3be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834865"
---
# <a name="parallel"></a>并行程序


TAEF 提供一种在多个处理器上并行执行测试的机制。

## <a name="span-idparallelism_guaranteesspanspan-idparallelism_guaranteesspanspan-idparallelism_guaranteesspanparallelism-guarantees"></a><span id="Parallelism_Guarantees"></span><span id="parallelism_guarantees"></span><span id="PARALLELISM_GUARANTEES"></span>并行性保证


-   不会同时执行两个未 [标记为可并行化](#markingtestsasparallelizable) 的测试。
-   并行测试可以同时与其他并行和非并行测试一起运行。
-   所有模块/类/测试设置和清理将在同一进程中的相关测试前后以线性方式运行。
-   如果模块或类至少包含一个并行测试，则可能会在不同的进程上并行执行模块/类安装程序。
-   并行执行模式与 [**"/inproc"**](executing-tests.md) 执行机制不兼容。

## <a name="span-idmarkingtestsasparallelizablespanspan-idmarkingtestsasparallelizablespanspan-idmarkingtestsasparallelizablespanmarking-tests-as-parallelizable"></a><span id="MarkingTestsAsParallelizable"></span><span id="markingtestsasparallelizable"></span><span id="MARKINGTESTSASPARALLELIZABLE"></span>将测试标记为可并行化


本机代码 (示例) ：

```cpp
class MyTests
{

    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(ParallelTest)
        TEST_METHOD_PROPERTY(L"Parallel", L"true")
    END_TEST_METHOD()
};
```

与 TAEF 中的其他通用元数据一样，可以在类或模块级别指定此项，& 将由此类或模块中包含的所有测试继承。 例如，若要将整个程序集标记为可并行化，可以在编译到测试 DLL 的 cpp 文件中的任何类或测试规范) 之外执行以下 (：

```cpp
BEGIN_MODULE()
    MODULE_PROPERTY(L"Parallel", L"true");
END_MODULE()
```

然后，可以在较小的范围内覆盖此范围更广的范围，以禁用特定测试用例或类的并行度，如下所示：

```cpp
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(NonParallelTest)
        TEST_METHOD_PROPERTY(L"Parallel", L"false");
    END_TEST_METHOD()
};
```

无论哪一项设置与测试方法最接近 (方法元数据都是最接近的类，然后使用模块) 来决定是否与其他测试并行运行此测试。

## <a name="span-idenablingparallelismatthecommandlinespanspan-idenablingparallelismatthecommandlinespanspan-idenablingparallelismatthecommandlinespanenabling-parallelism-at-the-command-prompt"></a><span id="EnablingParallelismAtTheCommandLine"></span><span id="enablingparallelismatthecommandline"></span><span id="ENABLINGPARALLELISMATTHECOMMANDLINE"></span>在命令提示符下启用并行


并行执行是一项可选功能。 尽管可将测试标记为并行，TAEF 仍将继续以线性方式执行测试，除非在命令提示符下启用了并行执行模式：

``` syntax
te unittests\* /parallel
```

 

 





