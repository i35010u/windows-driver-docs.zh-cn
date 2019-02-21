---
title: 用户模式监视器
description: 用户模式监视器
ms.assetid: CE6CEC2C-5E8E-40aa-A5D3-0062D6F82EFE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fbd12a98997fda7ecc2470aed5ba61ee3d27f1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527058"
---
# <a name="user-mode-monitor"></a>用户模式监视器


用户模式监视器允许测试，以获取更多上下文有关执行的处理待测试以获取更多上下文用于调查测试失败，或启用更好地验证从现有测试。 当前的用户模式监视器实现提供基本实现，具有更多自定义和配置的后续版本。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>简介


低级别的 Windows API 的通知的所有调试器事件的来源于给定进程的用户模式监视器 (UMM) 使用线程启动和停止、 模块加载、 崩溃，并处理异常等。 一旦收到调试器事件 UMM 代码可以执行以下某项操作，包括日志记录注释、 日志记录 （若要使测试未通过） 的错误，或甚至采取下过程测试的小型转储。

## <a name="span-idenablingtheusermodemonitorspanspan-idenablingtheusermodemonitorspanspan-idenablingtheusermodemonitorspanenabling-the-user-mode-monitor"></a><span id="Enabling_the_User_Mode_Monitor"></span><span id="enabling_the_user_mode_monitor"></span><span id="ENABLING_THE_USER_MODE_MONITOR"></span>启用用户模式监视器


若要启用为给定的测试用例 UMM，您需要提供两项配置：

1.  测试必须标记有 ProcessUnderTest 元数据值。 这允许 UMM 标识所测试的进程。
2.  Te.exe 命令行应包含 / userModeMonitor 开启 UMM 功能。

使用 UMM 代码; 时，应考虑采取以下几点

1.  如果有命名进程在测试运行的多个实例，然后发现实例第一次将使用。
2.  正在执行测试自动化的用户必须具有足够的权限来接收来自下过程测试的调试器事件。
3.  UMM 代码将后附加到进程在测试执行所有安装程序装置，和分离执行清理装置之前。 这样，测试的安装程序装置启动过程下测试，并执行任何必要的初始化测试准备。

## <a name="span-idsupportedusermodemonitoractionsspanspan-idsupportedusermodemonitoractionsspanspan-idsupportedusermodemonitoractionsspansupported-user-mode-monitor-actions"></a><span id="Supported_User_Mode_Monitor__Actions_"></span><span id="supported_user_mode_monitor__actions_"></span><span id="SUPPORTED_USER_MODE_MONITOR__ACTIONS_"></span>支持用户模式监视器操作


用户模式监视器具有一组给定的调试器事件发生在受监视的进程中时可能需要的操作。 在当前实现中，给定的事件将只调用它的默认操作;当前没有配置支持。

| 操作     | 描述                                                            |
|------------|------------------------------------------------------------------------|
| LogComment | 将注释添加到包含从该事件的上下文信息的日志。 |
| LogError   | 将错误记录到日志，则当前的测试将失败。            |
| 小型转储   | 写出一个小型转储并将其保存到日志。                         |
| 忽略     | 没有任何影响。                                                          |

 

## <a name="span-idsupportedusermodemonitoreventsspanspan-idsupportedusermodemonitoreventsspanspan-idsupportedusermodemonitoreventsspansupported-user-mode-monitor-events"></a><span id="Supported_User_Mode_Monitor__Events_"></span><span id="supported_user_mode_monitor__events_"></span><span id="SUPPORTED_USER_MODE_MONITOR__EVENTS_"></span>支持用户模式监视器事件


用户模式监视器呈现可以应用一个未列出，请更高版本的操作的事件。 下表显示了当前报告的事件，以及默认收到事件时将执行的操作的列表。

| 事件                                | 默认操作 （第二次机会默认操作） |
|--------------------------------------|-----------------------------------------------|
| 创建线程                        | 忽略                                        |
| 退出线程                          | 忽略                                        |
| 创建进程                       | 忽略                                        |
| 退出进程                         | LogError                                      |
| 负载模块                          | LogComment                                    |
| 卸载模块                        | 忽略                                        |
| 系统错误                         | 忽略                                        |
| 初始断点                   | LogError                                      |
| 初始模块加载                  | 忽略                                        |
| 调试对象输出                      | LogComment                                    |
| 访问冲突                     | LogError (LogError)                           |
| 断言失败                    | LogError (LogError)                           |
| 应用程序挂起                     | LogError (LogError)                           |
| 异常中断指令          | LogError                                      |
| 中断指令异常继续 | 忽略                                        |
| C + + EH 异常                     | LogError (LogError)                           |
| CLR 异常                        | LogError (LogError)                           |
| CLR 通知异常           | LogError （忽略）                             |
| 控制 LogError 异常           | LogError                                      |
| 控制 LogError 异常继续  | 忽略                                        |
| 控制 C 异常                  | LogError                                      |
| 控制 C 异常继续         | 忽略                                        |
| 数据未对齐                      | LogError (LogError)                           |
| 调试器命令异常           | 忽略                                        |
| 防护页冲突                 | LogError (LogError)                           |
| 非法指令                  | LogError (LogError)                           |
| 页 I/O 错误                    | LogError (LogError)                           |
| 整数的被零除               | LogError (LogError)                           |
| 整数溢出                     | LogError (LogError)                           |
| 无效的句柄                       | LogError                                      |
| 无效的句柄继续              | LogError                                      |
| 无效的锁定顺序                | LogError (LogError)                           |
| 无效的系统调用                  | LogError (LogError)                           |
| 断开连接的端口                    | LogError (LogError)                           |
| 服务挂起                         | LogError (LogError)                           |
| 单步执行异常                | LogError                                      |
| 继续单步执行异常       | 忽略                                        |
| 堆栈缓冲区溢出                | LogError (LogError)                           |
| 堆栈溢出                       | LogError (LogError)                           |
| 验证器停止                        | LogError (LogError)                           |
| Visual c + + 异常                 | 忽略 （忽略）                               |
| 唤醒调试器                        | LogError (LogError)                           |
| WOW64 断点                     | LogError （忽略）                             |
| WOW64 单步执行异常          | LogError （忽略）                             |
| 其他异常                      | LogError (LogError)                           |

 

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


为了说明使用 UMM 功能，让我们看看可自动执行 MSPaint 的测试 （略有精心设计的） 示例：

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
            // Close the &#39;mspaint under test&#39; - if it&#39;s already gone, this will throw, but that&#39;s no big deal.
            this.mspaintUnderTest.CloseMainWindow();
        }

        [TestMethod]
        [TestProperty("ProcessUnderTest", "mspaint.exe")]
        [TestProperty("Description", "Shows how a test can be failed if the UI is closed from underneath the test.")]
        public void SimpleInteraction()
        {
            Log.Comment("If the &#39;user mode monitor&#39; is enabled and mspaint.exe is closed,&quot;);
            Log.Comment(&quot;then this test will be failed.&quot;);
            Log.Comment("Sleeping for 5 seconds");

            Thread.Sleep(TimeSpan.FromSeconds(5));
        }

        private Process mspaintUnderTest;
    }
}
```

下面是快速测试结构的细分：

-   SimpleInteraction 测试表示与基于 UI 应用程序交互的测试-在这种情况下它是"MSPaint.exe"。 请注意，"ProcessUnderTest"元数据应用来调用此测试测试"mspaint.exe"过程。
-   测试必须确保认为存在没有预先存在的实例运行，并将启动要测试的单个实例的安装程序装置。
-   该测试还具有用于关闭在安装装置中启动的实例的清理装置。

测试操作非常简单，让我们看一下可能的结果：

1.  测试运行没有问题。 这是最佳的可能结果。
2.  没有启用 UMM，用户在执行过程中关闭 MSPaint 实例。 在这种情况下，该测试将通过，但清理将失败，并 InvalidOperationException。
3.  与 UMM 启用，用户在执行过程中关闭 MSPaint 实例。 在这种情况下，UMM 代码将记录错误显示进程关闭在测试失败。 清理无法正常工作，如用例 (2) 中所示。

与启用 UMM，错误行为立即报告并直接影响的测试结果。 由于早期提供可能和额外的上下文来帮助进行调试或了解测试失败报告错误，这是一个多更好的测试模式。

 

 





