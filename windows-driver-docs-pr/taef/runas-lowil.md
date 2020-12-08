---
title: RunAs LowIL
description: TAEF 在低完整性级别进程内运行测试。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99c0b34267daaff14d7613fc4795c06be5963737
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805923"
---
# <a name="runas-lowil"></a>RunAs LowIL


TAEF 在低完整性级别进程内运行测试。

**注意**  

 

**注意**  在运行早于 Windows Vista 的 Windows 版本的计算机上，不支持此选项。

 

## <a name="span-idspecifying_runas_on_the_command_line_spanspan-idspecifying_runas_on_the_command_line_spanspan-idspecifying_runas_on_the_command_line_spanspecifying-runas-on-the-command-line"></a><span id="Specifying_RunAs_on_the_Command_Line_"></span><span id="specifying_runas_on_the_command_line_"></span><span id="SPECIFYING_RUNAS_ON_THE_COMMAND_LINE_"></span>在命令行上指定 RunAs


``` syntax
te unittests\* /runas:lowil
```

## <a name="span-idmarking_tests_with_runas_spanspan-idmarking_tests_with_runas_spanspan-idmarking_tests_with_runas_spanmarking-tests-with-runas"></a><span id="Marking_Tests_with_RunAs_"></span><span id="marking_tests_with_runas_"></span><span id="MARKING_TESTS_WITH_RUNAS_"></span>用 RunAs 标记测试


测试元数据可用于指定程序集、类或测试方法的运行方式类型。

**注意**  在元数据中指定的 RunAs 值将替代在命令行上指定的 RunAs 值。 例如，使用 **runas：系统** 测试元数据标记的测试仍将作为本地系统运行，即使在命令行上指定了 **/runas：提升** 。

 

本机代码 (示例) 

```ManagedCPlusPlus
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(LowILTest)
        TEST_METHOD_PROPERTY(L"RunAs", L"LowIL")
    END_TEST_METHOD()
};
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[RunAs](runas.md)

 

 






