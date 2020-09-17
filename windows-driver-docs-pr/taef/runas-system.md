---
title: RunAs System
description: TAEF 将测试作为本地系统运行。
ms.assetid: E1138F36-D043-458A-8424-C649854CB7EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f1e52bf8cb9d14975a1a43906d79677f5c26c92
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715040"
---
# <a name="runas-system"></a>RunAs System


TAEF 将测试作为本地系统运行。

**注意**   作为 "本地系统" 运行的测试不应创建 (UI) 的任何用户界面。 如果测试需要创建 UI 或与 UI 交互，则需要将与 UI 相关的代码移到使用 [**CreateProcessAsUser 函数**](/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessasusera)在桌面上启动的独立可执行文件。

 

## <a name="span-idspecifying_runas_on_the_command_line_spanspan-idspecifying_runas_on_the_command_line_spanspan-idspecifying_runas_on_the_command_line_spanspecifying-runas-on-the-command-line"></a><span id="Specifying_RunAs_on_the_Command_Line_"></span><span id="specifying_runas_on_the_command_line_"></span><span id="SPECIFYING_RUNAS_ON_THE_COMMAND_LINE_"></span>在命令行上指定 RunAs


``` syntax
te unittests\* /runas:system
```

## <a name="span-idmarking_tests_with_runas_spanspan-idmarking_tests_with_runas_spanspan-idmarking_tests_with_runas_spanmarking-tests-with-runas"></a><span id="Marking_Tests_with_RunAs_"></span><span id="marking_tests_with_runas_"></span><span id="MARKING_TESTS_WITH_RUNAS_"></span>用 RunAs 标记测试


测试元数据可用于指定程序集、类或测试方法的运行方式类型。

**注意**   在元数据中指定的 RunAs 值将替代在命令行上指定的 RunAs 值。 例如，使用 **runas：系统** 测试元数据标记的测试仍将作为本地系统运行，即使在命令行上指定了 **/runas：提升** 。

 

本机代码 (示例) 

```ManagedCPlusPlus
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(SystemTest)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()
};
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[RunAs](runas.md)

 

