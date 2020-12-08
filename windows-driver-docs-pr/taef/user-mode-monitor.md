---
title: 用户模式监视器
description: 用户模式监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4f7730214335dc9de58eec051c0e1dd7d373f11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816461"
---
# <a name="user-mode-monitor"></a>用户模式监视器


用户模式监视器允许测试获取有关执行 "受测进程" 的详细信息，以便获取用于调查测试失败的更多上下文，或实现从现有测试进行更好的验证。 当前用户模式监视器实现提供了基本实现，并在后续版本中提供了更多的自定义和配置。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>简介


用户模式监视器 (嗯) 使用低级别 Windows API 来接收源自给定进程的所有 "调试器" 事件，即线程开始和停止、模块加载、崩溃和处理异常，只需对其进行命名。 收到调试程序事件后，嗯代码可以执行多个操作，包括记录注释、记录错误 (以便使测试) 失败，甚至获取所测试进程的小型转储。

## <a name="span-idenabling_the_user_mode_monitorspanspan-idenabling_the_user_mode_monitorspanspan-idenabling_the_user_mode_monitorspanenabling-the-user-mode-monitor"></a><span id="Enabling_the_User_Mode_Monitor"></span><span id="enabling_the_user_mode_monitor"></span><span id="ENABLING_THE_USER_MODE_MONITOR"></span>启用用户模式监视器


若要为给定的测试用例启用嗯，需要提供两个配置片段：

1.  测试必须标记有 "ProcessUnderTest" 元数据值。 这允许嗯标识要测试的进程。
2.  Te.exe 命令行应包括 "/userModeMonitor" 以打开嗯功能。

使用嗯代码时，应考虑以下几点：

1.  如果正在运行测试的命名进程有多个实例，则将使用首先发现的实例。
2.  执行测试自动化的用户必须具有足够的权限来接收受测进程中的调试器事件。
3.  执行所有安装程序夹具后，嗯代码将 "附加" 到受测进程，并在执行清理装置前 "分离"。 这允许测试的设置装置启动受测进程，并执行任何必要的初始化来为测试做好准备。

## <a name="span-idsupported_user_mode_monitor__actions_spanspan-idsupported_user_mode_monitor__actions_spanspan-idsupported_user_mode_monitor__actions_spansupported-user-mode-monitor-actions"></a><span id="Supported_User_Mode_Monitor__Actions_"></span><span id="supported_user_mode_monitor__actions_"></span><span id="SUPPORTED_USER_MODE_MONITOR__ACTIONS_"></span>支持的用户模式监视器 "操作"


当监视的进程中发生给定调试器事件时，用户模式监视器具有一组 "操作"。 在当前实现中，给定事件只会调用其默认操作;当前没有配置支持。

| 操作     | 描述                                                            |
|------------|------------------------------------------------------------------------|
| LogComment | 向日志添加注释，其中包含来自事件的上下文信息。 |
| LogError   | 将错误记录到日志中，这将导致当前测试失败。            |
| 附带   | 写出小型转储，并将其保存到日志中。                         |
| 忽略     | 不执行任何操作。                                                          |

 

## <a name="span-idsupported_user_mode_monitor__events_spanspan-idsupported_user_mode_monitor__events_spanspan-idsupported_user_mode_monitor__events_spansupported-user-mode-monitor-events"></a><span id="Supported_User_Mode_Monitor__Events_"></span><span id="supported_user_mode_monitor__events_"></span><span id="SUPPORTED_USER_MODE_MONITOR__EVENTS_"></span>支持的用户模式监视器 "事件"


用户模式监视器可应用上面列出的 "操作" 之一的 "事件"。 下表显示了报告事件的当前列表，以及接收事件时将执行的默认操作。

| 事件                                | 默认操作 (第二次机会默认操作)  |
|--------------------------------------|-----------------------------------------------|
| 创建线程                        | 忽略                                        |
| 退出线程                          | 忽略                                        |
| 创建进程                       | 忽略                                        |
| 退出进程                         | LogError                                      |
| 加载模块                          | LogComment                                    |
| 卸载模块                        | 忽略                                        |
| 系统错误                         | 忽略                                        |
| 初始断点                   | LogError                                      |
| 初始模块加载                  | 忽略                                        |
| 调试对象输出                      | LogComment                                    |
| 访问冲突                     | LogError (LogError)                            |
| 断言失败                    | LogError (LogError)                            |
| 应用程序挂起                     | LogError (LogError)                            |
| 中断指令异常          | LogError                                      |
| 中断指令异常继续 | 忽略                                        |
| C + + EH 异常                     | LogError (LogError)                            |
| CLR 异常                        | LogError (LogError)                            |
| CLR 通知异常           | LogError (忽略)                              |
| Control-LogError 异常           | LogError                                      |
| Control-LogError 异常继续  | 忽略                                        |
| Control-C 异常                  | LogError                                      |
| Control-C 异常继续         | 忽略                                        |
| 数据未对齐                      | LogError (LogError)                            |
| 调试器命令异常           | 忽略                                        |
| 保护页冲突                 | LogError (LogError)                            |
| 非法指令                  | LogError (LogError)                            |
| 页内 i/o 错误                    | LogError (LogError)                            |
| 整数被零除               | LogError (LogError)                            |
| 整数溢出                     | LogError (LogError)                            |
| 句柄无效                       | LogError                                      |
| 句柄继续无效              | LogError                                      |
| 锁定顺序无效                | LogError (LogError)                            |
| 系统调用无效                  | LogError (LogError)                            |
| 端口断开连接                    | LogError (LogError)                            |
| 服务挂起                         | LogError (LogError)                            |
| 单步例外                | LogError                                      |
| 单步异常继续       | 忽略                                        |
| 堆栈缓冲区溢出                | LogError (LogError)                            |
| 堆栈溢出                       | LogError (LogError)                            |
| 验证程序停止                        | LogError (LogError)                            |
| Visual C++ 异常                 | 忽略 (忽略)                                |
| 唤醒调试器                        | LogError (LogError)                            |
| WOW64 断点                     | LogError (忽略)                              |
| WOW64 单步异常          | LogError (忽略)                              |
| 其他异常                      | LogError (LogError)                            |

 

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


为了说明嗯功能的使用，我们来看一看 (略微) 精心设计的测试示例，该测试会自动执行 "Mspaint.exe"：

```cpp
namespace UserModeMonitorExample
{
    using System;
    using System.Diagnostics;
    using System.Threading;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using WEX.Logging.Interop;
    using WEX.TestExecution;

    [TestClass]
    public class BasicExample
    {
        [TestInitialize]
        public void TestInitialize()
        {
            Process[] runningPaintInstances = Process.GetProcessesByName("mspaint.exe");

            Verify.IsTrue(runningPaintInstances.Length == 0, "There are no running instances of mspaint.exe");

            this.mspaintUnderTest = Process.Start("mspaint.exe");
        }

        [TestCleanup]
        public void TestCleanup()
        {
            // Close the 'mspaint under test' - if it's already gone, this will throw, but that's no big deal.
            this.mspaintUnderTest.CloseMainWindow();
        }

        [TestMethod]
        [TestProperty("ProcessUnderTest", "mspaint.exe")]
        [TestProperty("Description", "Shows how a test can be failed if the UI is closed from underneath the test.")]
        public void SimpleInteraction()
        {
            Log.Comment("If the 'user mode monitor' is enabled and mspaint.exe is closed,");
            Log.Comment("then this test will be failed.");
            Log.Comment("Sleeping for 5 seconds");

            Thread.Sleep(TimeSpan.FromSeconds(5));
        }

        private Process mspaintUnderTest;
    }
}
```

下面是测试结构的快速细目：

-   "SimpleInteraction" 测试表示一个测试，该测试与基于 UI 的应用程序交互-在本例中为 "MSPaint.exe"。 请注意，已应用 "ProcessUnderTest" 元数据以调用此测试正在测试 "mspaint.exe" 进程。
-   该测试具有设置装置，可确保没有正在运行的预先存在的实例，并启动单个实例进行测试。
-   该测试还具有清理装置，用于关闭安装装置中启动的实例。

"测试" 是一种非常直接的操作，让我们看看可能的结果：

1.  测试运行不会出现问题。 这是可能的最佳结果。
2.  如果未启用嗯，用户会在执行期间关闭 Mspaint.exe 实例。 在这种情况下，测试将通过，但清理将失败，并出现 "InvalidOperationException"。
3.  启用嗯后，用户会在执行期间关闭 Mspaint.exe 实例。 在这种情况下，嗯代码将记录一个错误，该错误显示进程已关闭测试失败。 如果 (2) ，则清理会失败。

如果启用了嗯，则会立即报告残存错误行为，并直接影响测试结果。 这是一种更好的测试模式，因为错误会尽早报告并提供额外的上下文来帮助调试或了解测试失败。

 

 





