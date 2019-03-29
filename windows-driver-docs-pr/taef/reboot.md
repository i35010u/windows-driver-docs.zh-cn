---
title: 重新启动
description: 重新启动
ms.assetid: 8AB66CAB-9BAA-4911-A143-618627226B78
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02549bbc4e798526fdf37bf50ff97bb42084d6bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561588"
---
# <a name="reboot"></a>重新启动


TAEF 允许一个测试，以指定它会导致或需要重启计算机。 该功能的两到三个组件组成： 元数据标记为可能导致或要求重启，一个 API，用于请求 TAEF 执行重启或通知 TAEF 的即将发生测试启动重启和命令选项，可以选择将运行这些测试当执行本地测试。

## <a name="span-idbehaviorrebootspanspan-idbehaviorrebootspanbehavior"></a><span id="behavior_reboot"></span><span id="BEHAVIOR_REBOOT"></span>行为


重新启动计算机的特定语义需要对 TAEF 执行模型、 设置和清理操作的保证以及成功和失败行为的某些更改。

-   重新启动行为才可用 （包含相应的元数据），不到装置 （设置和清理） 的测试。
-   如果重新启动将使用该 API 从任何位置包含相应的标记测试以外，该函数将不会返回。 相反，TAEF 可终止测试进程。 应修复此表示一个写入测试的方式和测试代码中的 bug。
-   重启边界上，将运行测试装置。 这意味着拆解操作不会运行 （不管是否测试启动重新启动，或请求 TAEF 会导致重新启动本身） 重启前而不会在重新启动后运行安装程序操作。
-   日志记录 （并因此日志故障） 将被忽略的通知或请求重新启动，直到测试完成的时间。

## <a name="span-idmetadatarebootspanspan-idmetadatarebootspanmetadata"></a><span id="metadata_reboot"></span><span id="METADATA_REBOOT"></span>元数据


若要启用重新启动 Api 使用，应将测试标记通过设置**RebootPossible**元数据 **"true"**。 此元数据遵循元数据继承的常用规则，因此它可以指定在类级别如果在类中的任何测试可能会重启 （尽管由于而不是重量级性质的重新启动，它会建议明确确定有关哪些测试可以不能启动重新启动)。 请参阅上的文档[c + + 中创作测试](authoring-tests-in-c--.md)并[创作中的测试C#](authoring-tests-in-c-.md)有关的元数据规范示例。

## <a name="span-idapirebootspanspan-idapirebootspanapi"></a><span id="api_reboot"></span><span id="API_REBOOT"></span>API


有两个主要功能，用于处理计算机重启：

-   **Reboot(Option)** TAEF 启动测试计算机重新启动的请求。
-   **RebootCustom(Option)** 通知 TAEF 测试将会导致重新启动测试计算机。 此 API 还支持在系统发生崩溃。 TAEF 将确保适用的数据被刷新后，API 返回。

**选项**参数指定的恢复行为，之一：

-   **重新运行**，从而导致 TAEF 若要在发生重新启动后再次执行相同的测试
-   **继续**，从而导致 TAEF 发生重新启动后执行下一个测试

### <a name="span-idnativerebootspanspan-idnativerebootspannative"></a><span id="native_reboot"></span><span id="NATIVE_REBOOT"></span>本机

通过包括 Interruption.h 标头，然后调用函数访问重新启动 Api **WEX::TestExecution::Interruption**命名空间。 四个可能调用是：

```cpp
using namespace WEX::TestExecution;
Interruption::Reboot(RebootOption::Rerun);
Interruption::Reboot(RebootOption::Continue);
Interruption::RebootCustom(RebootOption::Rerun);
Interruption::RebootCustom(RebootOption::Continue);
```

### <a name="span-idmanagedrebootspanspan-idmanagedrebootspanmanaged"></a><span id="managed_reboot"></span><span id="MANAGED_REBOOT"></span>托管

中的两个方法调用**中断**静态类中的**WEX。TestExecution**命名空间，它位于**Te.Managed.dll**:

```cpp
using WEX.TestExecution;
Interruption.Reboot(RebootOption.Rerun);
Interruption.Reboot(RebootOption.Continue);
Interruption.RebootCustom(RebootOption.Rerun);
Interruption.RebootCustom(RebootOption.Continue);
```

## <a name="span-idpromptrebootspanspan-idpromptrebootspancommand-prompt-usage"></a><span id="prompt_reboot"></span><span id="PROMPT_REBOOT"></span>命令提示符下使用情况


此功能的理想的使用是运行 TAEF 测试，将使用可能会重启[跨机器执行](cross-machine-execution.md)或通过 WTT。 在这些情况下 TAEF 启用重新启动执行隐式\*因为它应不会中断您的工作流。 如果您在执行重新启动测试手动在本地计算机上或者需要重写 TAEF 使用来缓存其状态的默认路径，将需要显式选择启用重新启动测试。 如果不这样做，则重新启动的任何测试会标记为已阻止。 若要启用重新启动测试执行本地时，请使用以下命令参数：

``` syntax
Te.exe /rebootStateFile:MyRestartFile.xml
```

TAEF 将创建指定用来存储其状态的文件 (其中已经过测试执行，任何 TAEF 命令或环境选项，等等) 并从中重新启动后的恢复时从中断处恢复。 TAEF 处理计算机后重新执行本身后重新启动。

请注意，此选项不会不起作用由于 TAEF 取决于重新启动 （RunOnce 项） 后继续测试功能删除的 ARM 计算机上。

\* 只要您没有使用任何不兼容的执行功能 (目前[并行](parallel.md)并[测试模式](test-modes.md))。

## <a name="span-idfaqsrebootspanspan-idfaqsrebootspanfrequently-asked-questions"></a><span id="faqs_reboot"></span><span id="FAQS_REBOOT"></span>方面的常见问题


### <a name="span-idrerunfaqspanspan-idrerunfaqspanif-i-choose-rerun-is-there-any-way-i-can-tell-whether-the-test-is-being-invoked-for-the-first-time-or-after-a-restart"></a><span id="rerun_faq"></span><span id="RERUN_FAQ"></span>如果我选择重新运行，有没有办法可以知道在第一次或重启后是否调用测试？

TAEF 不提供任何功能，从而实现此目的。 重新运行选项旨在使您能够编写测试，可能需要重新启动基于状态的计算机 （如运行 Windows 更新） 的数目不确定。 请考虑使用[ExecutionGroup](execution-groups.md)和分解为单独的测试操作之前/之后重新启动序列中出现的任务继续选项。

### <a name="span-idothertestsfaqspanspan-idothertestsfaqspanwhich-taef-test-types-are-supported"></a><span id="othertests_faq"></span><span id="OTHERTESTS_FAQ"></span>支持哪些 TAEF 测试类型？

此功能可为本机，管理，并且脚本测试。

 

 





