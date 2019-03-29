---
title: RunAs Restricted
description: TAEF 可确保在受限制的进程中运行测试。
ms.assetid: 1565344E-2CF9-4E08-9BA2-23FE1D677ABA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 046f3937f203a9b8d18114e8cc62eedcdafa9f0e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577463"
---
# <a name="runas-restricted"></a>RunAs Restricted


TAEF 可确保在受限制的进程中运行测试。

**请注意**  必须运行版本早于 Windows Vista 的 Windows 的计算机上，从一个管理员进程中运行受限制的测试。

 

## <a name="span-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspecifying-runas-on-the-command-line"></a><span id="Specifying_RunAs_on_the_Command_Line_"></span><span id="specifying_runas_on_the_command_line_"></span><span id="SPECIFYING_RUNAS_ON_THE_COMMAND_LINE_"></span>在命令行上指定运行方式


``` syntax
te unittests\* /runas:restricted
```

## <a name="span-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanmarking-tests-with-runas"></a><span id="Marking_Tests_with_RunAs_"></span><span id="marking_tests_with_runas_"></span><span id="MARKING_TESTS_WITH_RUNAS_"></span>将标记与运行方式的测试


测试元数据可用于指定程序集、 类或测试方法的运行方式类型。

**请注意**  元数据中指定的运行方式值重写命令行上指定的运行方式值。 例如，测试标有**runas:system**测试元数据仍将运行作为本地系统，即使 **/runas:elevated**命令行上指定。

 

示例 （本机代码）

```ManagedCPlusPlus
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(RestrictedTest)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
    END_TEST_METHOD()
};
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[RunAs](runas.md)

 

 






