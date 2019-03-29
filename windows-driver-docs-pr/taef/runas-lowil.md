---
title: RunAs LowIL
description: TAEF 运行低完整性级别进程内的测试。
ms.assetid: 8FF26AB3-F473-4352-8951-D3F7DF366B5F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b920fcec53aa336f42e833ea175ed68cd9ab355
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561587"
---
# <a name="runas-lowil"></a>RunAs LowIL


TAEF 运行低完整性级别进程内的测试。

**注意**  

 

**请注意**  上运行版本早于 Windows Vista 的 Windows 的计算机，此选项不支持。

 

## <a name="span-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspecifying-runas-on-the-command-line"></a><span id="Specifying_RunAs_on_the_Command_Line_"></span><span id="specifying_runas_on_the_command_line_"></span><span id="SPECIFYING_RUNAS_ON_THE_COMMAND_LINE_"></span>在命令行上指定运行方式


``` syntax
te unittests\* /runas:lowil
```

## <a name="span-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanmarking-tests-with-runas"></a><span id="Marking_Tests_with_RunAs_"></span><span id="marking_tests_with_runas_"></span><span id="MARKING_TESTS_WITH_RUNAS_"></span>将标记与运行方式的测试


测试元数据可用于指定程序集、 类或测试方法的运行方式类型。

**请注意**  元数据中指定的运行方式值重写命令行上指定的运行方式值。 例如，测试标有**runas:system**测试元数据仍将运行作为本地系统，即使 **/runas:elevated**命令行上指定。

 

示例 （本机代码）

```ManagedCPlusPlus
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(LowILTest)
        TEST_METHOD_PROPERTY(L"RunAs", L"LowIL")
    END_TEST_METHOD()
};
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[RunAs](runas.md)

 

 






