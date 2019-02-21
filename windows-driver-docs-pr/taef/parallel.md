---
title: 并行
description: 并行
ms.assetid: E2AF7B3A-B614-4fe1-9CFB-0860F68E895C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f3579444172825987cbde409823b564f3a8725d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521208"
---
# <a name="parallel"></a>并行


TAEF 提供了一种机制来跨多个处理器的并行执行测试。

## <a name="span-idparallelismguaranteesspanspan-idparallelismguaranteesspanspan-idparallelismguaranteesspanparallelism-guarantees"></a><span id="Parallelism_Guarantees"></span><span id="parallelism_guarantees"></span><span id="PARALLELISM_GUARANTEES"></span>并行性保证


-   没有两个测试未[标记为可并行化](#markingtestsasparallelizable)曾经将并发执行。
-   可以与其他并行和非并行测试同时运行并行测试。
-   所有模块/类/测试设置和清理将都运行以线性方式在同一进程中相关的测试之前和之后。
-   如果模块或类中包含至少一个并行测试，可能在不同进程并行执行模块/类安装程序。
-   并行执行模式是与不兼容[ **"/ inproc"** ](executing-tests.md)执行机制。

## <a name="span-idmarkingtestsasparallelizablespanspan-idmarkingtestsasparallelizablespanspan-idmarkingtestsasparallelizablespanmarking-tests-as-parallelizable"></a><span id="MarkingTestsAsParallelizable"></span><span id="markingtestsasparallelizable"></span><span id="MARKINGTESTSASPARALLELIZABLE"></span>将测试标记为可并行化


示例 （本机代码）：

```cpp
class MyTests
{

    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(ParallelTest)
        TEST_METHOD_PROPERTY(L"Parallel", L"true")
    END_TEST_METHOD()
};
```

如同 TAEF 中其他常规元数据，这可以在类或模块级别指定和将继承该类或模块中包含的所有测试。 例如，若要将标记为可并行化整个程序集可以执行以下 （之外任何类或测试规范） 在 cpp 文件编译到您的测试 DLL:

```cpp
BEGIN_MODULE()
    MODULE_PROPERTY(L"Parallel", L"true");
END_MODULE()
```

然后，此更广范围可以是在较小作用域，以禁用并行操作的特定测试用例或类，如下所示重写：

```cpp
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(NonParallelTest)
        TEST_METHOD_PROPERTY(L"Parallel", L"false");
    END_TEST_METHOD()
};
```

无论设置是最接近的测试方法 （方法元数据为最接近，则类，则模块） 将用于确定是否在使用其他测试来并行运行此测试。

## <a name="span-idenablingparallelismatthecommandlinespanspan-idenablingparallelismatthecommandlinespanspan-idenablingparallelismatthecommandlinespanenabling-parallelism-at-the-command-prompt"></a><span id="EnablingParallelismAtTheCommandLine"></span><span id="enablingparallelismatthecommandline"></span><span id="ENABLINGPARALLELISMATTHECOMMANDLINE"></span>在命令提示符下启用并行度


并行执行是一项选择加入的功能。 尽管可以将测试标记为并行，TAEF 将继续以线性方式执行测试，除非在命令提示符下启用并行执行模式：

``` syntax
te unittests\* /parallel
```

 

 





