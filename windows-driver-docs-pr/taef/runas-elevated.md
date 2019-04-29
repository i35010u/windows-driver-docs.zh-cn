---
title: RunAs Elevated
description: TAEF 确保生成已提升的进程以运行测试，如有必要在提升的进程中运行测试。
ms.assetid: 6292E431-6EB5-4962-BBB0-B86FC4CE4643
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b31b4353a29f00362cadf84322440197bd11e94d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380207"
---
# <a name="runas-elevated"></a>RunAs Elevated


TAEF 确保生成已提升的进程以运行测试，如有必要在提升的进程中运行测试。

**注意：执行 TAEF 的用户必须是 administrators 组的成员才能执行测试运行方式与标记 = 提升。** 这是由于非管理员不具有提升的拆分令牌。 如果非管理员尝试使用运行方式运行标记测试 = 提升，**测试将被标记为已阻止**。

**请注意**  运行版本早于 Windows Vista 的 Windows 的计算机上，你必须从一个管理员进程运行提升的测试。

 

## <a name="span-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspecifying-runas-on-the-command-line"></a><span id="Specifying_RunAs_on_the_Command_Line_"></span><span id="specifying_runas_on_the_command_line_"></span><span id="SPECIFYING_RUNAS_ON_THE_COMMAND_LINE_"></span>在命令行上指定运行方式


``` syntax
te unittests\* /runas:elevated
```

## <a name="span-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanmarking-tests-with-runas"></a><span id="Marking_Tests_with_RunAs_"></span><span id="marking_tests_with_runas_"></span><span id="MARKING_TESTS_WITH_RUNAS_"></span>将标记与运行方式的测试


测试元数据可用于指定程序集、 类或测试方法的运行方式类型。

**请注意**  元数据中指定的运行方式值重写命令行上指定的运行方式值。 例如，测试标有**runas:system**测试元数据仍将运行作为本地系统，即使 **/runas:elevated**命令行上指定。

 

示例 （本机代码）

```ManagedCPlusPlus
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(ElevatedTest)
        TEST_METHOD_PROPERTY(L"RunAs", L"Elevated")
    END_TEST_METHOD()
};
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[RunAs](runas.md)

 

 






