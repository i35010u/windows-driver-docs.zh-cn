---
title: 重新启动
description: 重新启动
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1103a6d687d3159e6a653e0c17576826052d04c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821183"
---
# <a name="reboot"></a>重新启动


TAEF 允许测试指定它可能会导致或要求计算机重新启动。 此功能包含两到三个组件：用于标记测试的元数据可能会导致或需要重新启动，这是一个 API，用于请求 TAEF 执行重启或通知 TAEF 即将开始的测试启动的重新启动，并使用命令选项来选择在本地执行时运行这些测试。

## <a name="span-idbehavior_rebootspanspan-idbehavior_rebootspanbehavior"></a><span id="behavior_reboot"></span><span id="BEHAVIOR_REBOOT"></span>操作


重新启动计算机的特定语义需要对 TAEF 执行模型进行一些更改、安装和清理操作的保证以及成功和失败行为。

-   重新启动行为仅适用于使用合适的元数据) 的测试 (，而不能用于 (安装和清理) 的装置。
-   如果重新启动 API 是使用适当标记的测试以外的任何位置使用的，则该函数将不会返回。 相反，TAEF 将终止测试过程。 这表示测试编写方式的 bug，应修复测试代码。
-   测试装置将不会在重新启动边界上运行。 这意味着，在重新启动之前不会运行拆卸操作 (无论测试是启动重新启动还是请求 TAEF 导致) 重新启动，都不会运行，而是在重启后不会运行安装操作。
-   日志记录 (和日志失败) 将在你通知或请求重新启动直到测试完成后才会被忽略。

## <a name="span-idmetadata_rebootspanspan-idmetadata_rebootspanmetadata"></a><span id="metadata_reboot"></span><span id="METADATA_REBOOT"></span>元数据


若要启用重新启动 Api，应通过将 **RebootPossible** 的元数据设置为 **"true"** 来标记测试。 此元数据服从元数据继承的常用规则，因此，如果您的类中的任何测试都可能重新 (启动，则可以在类级别指定该元数据; 但是，如果重启的性质相当高，则建议您明确决定哪些测试可以且不能启动重新启动) 。 有关元数据规范的示例，请参阅 [c + + 中的创作测试](authoring-tests-in-c--.md) 文档和 [在 c # 中创作测试](authoring-tests-in-c-.md) 。

## <a name="span-idapi_rebootspanspan-idapi_rebootspanapi"></a><span id="api_reboot"></span><span id="API_REBOOT"></span>API


用于处理计算机重新启动的主要函数有两个：

-   **重新启动 (选项)** 请求 TAEF 启动测试计算机的重新启动。
-   **RebootCustom (选项)** 通知 TAEF 测试将导致重新启动测试计算机。 此 API 还支持系统崩溃。 TAEF 将确保在 API 返回后刷新适用的数据。

**Option** 参数指定 resume 行为，其中之一为：

-   **重新运行**，导致 TAEF 在重新启动后再次执行相同的测试
-   **继续**，导致 TAEF 在重启后执行下一个测试

### <a name="span-idnative_rebootspanspan-idnative_rebootspannative"></a><span id="native_reboot"></span><span id="NATIVE_REBOOT"></span>本机

通过包含 **WEX：： testexecution.completed：：中断** 命名空间中的函数，来访问重新启动 api。 四个可能的调用为：

```cpp
using namespace WEX::TestExecution;
Interruption::Reboot(RebootOption::Rerun);
Interruption::Reboot(RebootOption::Continue);
Interruption::RebootCustom(RebootOption::Rerun);
Interruption::RebootCustom(RebootOption::Continue);
```

### <a name="span-idmanaged_rebootspanspan-idmanaged_rebootspanmanaged"></a><span id="managed_reboot"></span><span id="MANAGED_REBOOT"></span>经过

调用 WEX 中的 **中断** 静态类中的两个方法之一 **。Testexecution.completed** 命名空间，位于 **Te.Managed.dll** 中：

```cpp
using WEX.TestExecution;
Interruption.Reboot(RebootOption.Rerun);
Interruption.Reboot(RebootOption.Continue);
Interruption.RebootCustom(RebootOption.Rerun);
Interruption.RebootCustom(RebootOption.Continue);
```

## <a name="span-idprompt_rebootspanspan-idprompt_rebootspancommand-prompt-usage"></a><span id="prompt_reboot"></span><span id="PROMPT_REBOOT"></span>命令提示符用法


此功能的理想用法是运行可能会通过 [跨计算机执行](cross-machine-execution.md) 或通过 WTT 重启的 TAEF 测试。 在这些情况下，TAEF 将隐式启用重启执行， \* 因为它不应中断工作流。 如果要在本地计算机上手动执行重新启动测试，或需要重写 TAEF 用于缓存其状态的默认路径，则必须明确选择重新启动测试。 否则，任何重新启动测试将被标记为 "已阻止"。 若要在本地执行时启用重新启动测试，请使用以下命令参数：

``` syntax
Te.exe /rebootStateFile:MyRestartFile.xml
```

TAEF 将创建指定的文件，以存储其状态， (已执行的测试、任何 TAEF 命令或环境选项等，并在重新启动后恢复时，) 并从其停止的位置恢复。 TAEF 在计算机重新启动后再次启动时，将自动执行。

请注意，此选项不适用于 ARM 计算机，因为删除了 TAEF 依赖于在重新启动后恢复测试的功能 (RunOnce 键) 。

\*只要您不使用任何不兼容的执行功能 (当前的[并行](parallel.md)[模式和测试模式](test-modes.md)) 。

## <a name="span-idfaqs_rebootspanspan-idfaqs_rebootspanfrequently-asked-questions"></a><span id="faqs_reboot"></span><span id="FAQS_REBOOT"></span>常见问题


### <a name="span-idrerun_faqspanspan-idrerun_faqspanif-i-choose-rerun-is-there-any-way-i-can-tell-whether-the-test-is-being-invoked-for-the-first-time-or-after-a-restart"></a><span id="rerun_faq"></span><span id="RERUN_FAQ"></span>如果选择 "重新运行"，是否可以通过任何方式来确定是第一次还是在重启后调用该测试？

为实现此目的，TAEF 不提供任何功能。 重新运行选项的目的是使你能够根据 (计算机的状态（例如，运行 Windows 更新到完成) ）编写可能需要不确定的重新启动次数的测试。 请考虑使用 [ExecutionGroup](execution-groups.md) 和 continue 选项将任务分解为单独的测试操作，这些操作将在重新启动之前/之后按顺序发生。

### <a name="span-idothertests_faqspanspan-idothertests_faqspanwhich-taef-test-types-are-supported"></a><span id="othertests_faq"></span><span id="OTHERTESTS_FAQ"></span>支持哪些 TAEF 测试类型？

此功能适用于本机、托管和脚本测试。

 

 





