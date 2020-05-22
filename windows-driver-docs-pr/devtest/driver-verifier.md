---
title: 驱动程序验证程序
description: 驱动程序验证程序监视 Windows 内核模式驱动程序和图形驱动程序，目的是检测可能损坏系统的非法函数调用或操作。
ms.assetid: a8a78dde-930f-4d0b-be46-f7d07b0bf21b
keywords:
- 验证驱动程序 WDK，驱动程序验证程序
- 驱动程序验证 WDK，驱动程序验证程序
- 驱动程序验证程序 WDK
- 驱动程序验证程序 WDK，关于驱动程序验证程序
- 非法函数调用 WDK 驱动程序验证程序
- 压力测试 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ff9c842db8492481227caad55d09b53e264cd5f
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769395"
---
# <a name="driver-verifier"></a>驱动程序验证程序

驱动程序验证程序监视 Windows 内核模式驱动程序和图形驱动程序，目的是检测可能损坏系统的非法函数调用或操作。 驱动程序验证程序可将 Windows 驱动程序用于各种强调和测试，以找出不正确的行为。 你可以配置要运行的测试，这允许你通过繁重的负载或更精简的测试来放置驱动程序。 你还可以同时在多个驱动程序或一个驱动程序上运行驱动程序验证程序。

> [!Caution]
> <ul><li>运行驱动程序验证程序可能会导致计算机崩溃。</li>
> <li>只应在用于测试和调试的计算机上运行驱动程序验证程序。</li>
> <li>您必须是计算机上的管理员组才能使用驱动程序验证程序。</li>
> <li>驱动程序验证程序不包含在 Windows 10 中，因此我们建议改为在 Windows 10 上测试驱动程序的行为。</li></ul>


## <a name="where-can-i-download-driver-verifier"></a>在哪里可以下载驱动程序验证程序？

不需要下载驱动程序验证程序，因为它包含在%WinDir%\system32\ 中的大部分 Windows 版本中作为 Verifier。 （驱动程序验证程序不包含在 Windows 10 S 中。）驱动程序验证程序不会单独分发为下载包。

有关 Windows 10 和以前版本的 Windows 的驱动程序验证程序更改的信息，请参阅<a href="driver-verifier--what-s-new.md" data-raw-source="[Driver Verifier: What's New](driver-verifier--what-s-new.md)">驱动程序验证程序：新增功能</a>。


## <a name="when-to-use-driver-verifier"></a>何时使用驱动程序验证程序

在整个开发和测试驱动程序的过程中运行驱动程序验证程序。 更具体地说，将驱动程序验证程序用于以下目的：

-   若要在开发周期的早期发现问题，更容易且成本更低。

-   用于故障排除和调试测试失败和计算机崩溃。

-   监视使用 WDK、Visual Studio 和[windows 硬件实验室工具包](https://docs.microsoft.com/windows-hardware/test/hlk/)（windows HLK）或[Windows 硬件认证工具包](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))（适用于 Windows 8.1）的测试部署驱动程序时的行为。 有关测试驱动程序的详细信息，请参阅[测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver)。


## <a name="how-to-start-driver-verifier"></a>如何启动驱动程序验证程序

只应在测试计算机或要测试和调试的计算机上运行驱动程序验证程序。 若要充分利用驱动程序验证程序，你应该使用内核调试器并连接到测试计算机。 有关调试工具的详细信息，请参阅[适用于 Windows 的调试工具（WinDbg、KD、CDB、NTSD）](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

1. 通过选择 "以**管理员身份运行**" 启动**命令提示符**窗口，然后键入**Verifier**以打开**驱动程序验证器管理器**。

2. 选择 "**创建标准设置**（默认任务）"，然后单击 "**下一步**"。

   你还可以选择 "**创建自定义设置**" 从预定义的设置中进行选择，或选择单独的选项。 有关详细信息，请参阅[驱动程序验证程序选项和规则类](driver-verifier-options.md)和[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

3. 在 "**选择要验证的驱动程序**" 下，选择下表中所述的选择方案之一。

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">选项</th>
   <th align="left">建议用途</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><strong>自动选择未签名的驱动程序</strong></td>
   <td align="left"><p>适用于在运行不需要签名驱动程序的 Windows 版本的计算机上进行测试。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>自动选择为旧版 Windows 构建的驱动程序</strong></td>
   <td align="left"><p>用于测试与较新版本的 Windows 的驱动程序兼容性。</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><strong>自动选择在此计算机上安装的所有驱动程序</strong></td>
   <td align="left"><p>提供系统上所测试的驱动程序数量的最大覆盖范围。 对于驱动程序可以与系统上的其他设备或驱动程序交互的测试方案，此选项很有用。</p>
   <p>此选项还可以耗尽适用于<a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊池</a>和某些资源跟踪的资源。 测试所有驱动程序也可能会对系统性能产生不利影响。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>从列表中选择驱动程序名称</strong></td>
   <td align="left"><p>在大多数情况下，您需要指定要测试的驱动程序。</p>
   <p>如果选择设备堆栈中的所有驱动程序，则可以使用<a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">增强的 I/o 验证</a>选项跟踪对象和检查符合性，因为在堆栈中的每个驱动程序之间传递了一个 i/o 请求数据包（IRP），这允许在检测到错误时提供更详细的信息。</p>
   <p>如果您正在运行的测试方案可度量系统或驱动程序性能指标，或者您想要分配可用于检测内存损坏或资源跟踪问题（如死锁或互斥体）的最大资源数，请选择单个驱动程序。 当一次使用一个驱动程序时，<a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊池</a>和<a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">i/o 验证</a>选项更为有效。</p></td>
   </tr>
   </tbody>
   </table>


4. 如果选择**了 "从列表选择驱动程序名称**"，请单击 "**下一步**"，然后选择一个或多个特定驱动程序。

5. 单击 "**完成**"，然后重新启动计算机。



>[!Note]
> 你还可以在命令提示符窗口中运行驱动程序验证程序，而无需启动驱动程序验证程序管理器。 例如，若要在名为*myDriver*的驱动程序上运行带有标准设置的驱动程序验证程序，可以使用以下命令：
> ```console
> verifier /standard /driver myDriver.sys
> ```
>
> 有关命令行选项的详细信息，请参阅[**Driver Verifier 命令语法**](verifier-command-line.md)。



## <a name="how-to-control-driver-verifier"></a>如何控制驱动程序验证程序

您可以使用驱动程序验证器管理器或命令行来控制驱动程序验证程序。 若要启动驱动程序验证程序管理器，请参阅本主题前面的[如何启动驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier#how-to-start-driver-verifier)。

对于以下每项操作，可以使用驱动程序验证器管理器或输入命令行。


**停止或重置驱动程序验证程序**

1. 在**驱动程序验证器管理器**中，选择 "**删除现有设置**"，然后单击 "**完成**"。

    或

    在命令提示符处输入以下命令：

    ```console
    verifier /reset
    ```

2. 重新启动计算机。


**查看驱动程序验证程序统计信息**

- 在 "**驱动程序验证程序管理器**" 中，选择 **"显示有关当前已验证的驱动程序的信息**"，**然后单击 "** 继续单击 "**下一步**" 将显示其他信息。

  或

  在命令提示符处输入以下命令：

  ```console
  verifier /query
  ```


**查看驱动程序验证程序设置**

- 在**驱动程序验证器管理器**中，选择 "**显示现有设置**"，然后单击 "**下一步**"

  或

  在命令提示符处输入以下命令：

  ```console
  verifier /querysettings
  ```


## <a name="how-to-debug-driver-verifier-violations"></a>如何调试驱动程序验证程序冲突

若要充分利用驱动程序验证程序，你应该使用内核调试器并将其连接到测试计算机。 有关 Windows 调试工具的概述，请参阅适用[于 windows 的调试工具（WinDbg、KD、CDB、NTSD）](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

如果驱动程序验证程序检测到冲突，则会生成 bug 检查来停止计算机。 这是为了提供用于调试问题的最大信息。 如果已将内核调试器连接到运行驱动程序验证程序的测试计算机，并且 Driver Verifier 检测到冲突，则 Windows 将中断调试器并显示错误的简短说明。

驱动程序验证程序检测到的所有冲突都将导致 bug 检查。 常见的 bug 检查代码包括：

-   [**Bug 检查0xC1：特殊 \_ 池 \_ 检测到 \_ 内存 \_ 损坏**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc1--special-pool-detected-memory-corruption)
-   [**Bug 检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)
-   [**Bug 检查0xC6：驱动程序已 \_ 捕获 \_ 修改已释放的 \_ \_ 池**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc6--driver-caught-modifying-freed-pool)
-   [**Bug 检查0xC9：驱动程序 \_ 验证程序 \_ IOMANAGER \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc9--driver-verifier-iomanager-violation)
-   [**Bug 检查0xD6：在 \_ \_ \_ \_ \_ \_ 分配结束后出现驱动程序页错误**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xd6--driver-page-fault-beyond-end-of-allocation)
-   [**Bug 检查0xE6：驱动程序 \_ 验证程序 \_ DMA \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xe6--driver-verifier-dma-violation)

有关详细信息，请参阅[在启用驱动程序验证程序时处理 Bug 检查](https://docs.microsoft.com/windows-hardware/drivers/debugger/handling-a-bug-check-when-driver-verifier-is-enabled)。 有关调试 Bug 检查0xC4 的提示，请参阅[调试 Bug 检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突](debugging-bug-check-0xc4--driver-verifier-detected-violation.md)。

当你启动新的调试会话时，请使用调试器扩展命令 " [**！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)"。 在内核模式下，" **！分析**" 命令显示有关最新 bug 检查的信息。 若要显示*其他*信息，以帮助识别出错的驱动程序，请在**kd>** 提示符下向命令添加选项**v** ：

```dbgcmd
kd> !analyze -v
```

除了 **！分析**以外，还可以在**kd>** 提示符下输入以下调试器扩展，以查看特定于驱动程序验证程序的信息：

-   [**！ verifier**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-verifier)转储捕获的驱动程序验证程序统计信息。 使用 **！ verifier-？** 显示所有可用选项。

    ```dbgcmd
    kd> !verifier
    ```

-   [**！死锁**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-deadlock)显示了驱动程序验证程序的死锁检测功能跟踪的锁定或对象的相关信息。 使用 **！死锁-？** 显示所有可用选项。

    ```dbgcmd
    kd> !deadlock
    ```

-   [**！ iovirp**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-iovirp) \[*地址* \]显示与由 i/o 验证程序跟踪的 IRP 相关的信息。 例如：

    ```dbgcmd
    kd> !iovirp 947cef68
    ```

-   [**！ ruleinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo) \[*RuleID* \]显示与违反的[DDI 相容性检查](ddi-compliance-checking.md)规则相关的信息。 （*RuleID*始终是 bug 检查的第一个参数。）DDI 相容性检查中的所有规则 Id 的格式为 0x200*nn*。 例如：

    ```dbgcmd
    kd> !ruleinfo 0x20005
    ```


## <a name="related-topics"></a>相关主题

[驱动程序验证程序：新增功能](driver-verifier--what-s-new.md)

[驱动程序验证程序选项](driver-verifier-options.md)

[**驱动程序验证程序命令语法**](verifier-command-line.md)

[使用驱动程序验证程序](using-driver-verifier.md)

[控制驱动程序验证程序](controlling-driver-verifier.md)
