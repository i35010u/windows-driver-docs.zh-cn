---
title: 驱动程序验证程序
description: 驱动程序验证工具可监视 Windows 内核模式驱动程序和图形驱动程序以检测非法的函数调用或可能会损坏系统的操作。
ms.assetid: a8a78dde-930f-4d0b-be46-f7d07b0bf21b
keywords:
- 验证驱动程序 WDK，驱动程序验证程序
- 驱动程序验证 WDK，驱动程序验证程序
- 驱动程序验证程序 WDK
- 驱动程序验证程序 WDK，关于 Driver Verifier
- 非法的函数调用 WDK Driver Verifier
- 压力测试 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47de964f7acb1ed8414626d0fc9e663c6e67f7b4
ms.sourcegitcommit: e3cf7d69c13846f3e7ece2b6178ecec23b9854ae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65940375"
---
# <a name="driver-verifier"></a>驱动程序验证程序

驱动程序验证工具可监视 Windows 内核模式驱动程序和图形驱动程序以检测非法的函数调用或可能会损坏系统的操作。 驱动程序验证程序可以使用者各种压力和测试，以找到不正确的行为的 Windows 驱动程序。 你可以配置哪些测试运行，这使你可以通过超负荷加载或更多简化测试放置一个驱动程序。 您还可以运行驱动程序验证程序上多个驱动程序同时，或一个驱动程序上一次。

> [!Caution]
> <ul><li>运行驱动程序验证程序可能会导致计算机崩溃。</li>
> <li>您只应将用于测试和调试的计算机上运行驱动程序验证程序。</li>
> <li>您必须在计算机上 Administrators 组，使用驱动程序验证程序中。</li>
> <li>驱动程序验证程序不包括在 Windows 10 S，因此我们建议您改为测试 Windows 10 上的驱动程序行为。</li></ul>


## <a name="where-can-i-download-driver-verifier"></a>在何处可以下载驱动程序验证程序

您不必下载驱动程序验证程序，因为它是随大多数版本的 Windows 中作为 Verifier.exe %WinDir%\system32\。 （驱动程序验证程序不包含于 Windows 10 s。）驱动程序验证程序不是单独下载包进行分布。

有关驱动程序验证工具适用于 Windows 10 和 Windows 的早期版本中的更改的信息，请参阅<a href="driver-verifier--what-s-new.md" data-raw-source="[Driver Verifier: What's New](driver-verifier--what-s-new.md)">Driver Verifier:什么是新</a>。


## <a name="when-to-use-driver-verifier"></a>何时使用 Driver Verifier

在开发和测试您的驱动程序的整个运行驱动程序验证程序。 更具体地说，使用驱动程序验证程序实现以下目的：

-   若要早期阶段发现问题时更加容易，不在开发周期成本高昂，若要更正。

-   对于故障排除和调试测试故障和计算机崩溃。

-   若要监视部署用于测试使用 WDK 和 Visual Studio 中，从测试的驱动程序时的行为[Windows 硬件实验室套件](https://go.microsoft.com/fwlink/p/?linkid=254893)(Windows HLK) 或[Windows 硬件认证工具包](https://docs.microsoft.com/en-us/previous-versions/windows/hardware/hck/jj124227(v=vs.85))（适用于 Windows8.1)。 有关测试驱动程序的详细信息，请参阅[测试驱动程序](https://docs.microsoft.com/en-us/windows-hardware/drivers/develop/testing-a-driver)。


## <a name="how-to-start-driver-verifier"></a>如何启动驱动程序验证程序

在测试计算机上或在测试和调试的计算机上，应仅运行驱动程序验证程序。 若要从驱动程序验证程序获得最佳效果，应使用内核调试程序并连接到测试计算机。 有关调试工具的详细信息，请参阅[调试工具的 Windows （WinDbg、 KD、 CDB、 NTSD）](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/index)。

1. 启动**命令提示符**通过选择窗口**以管理员身份运行**，和类型**verifier**以打开**驱动程序验证程序管理器**。

2. 选择**创建标准设置**（默认任务），然后单击**下一步**。

   你还可以选择**创建自定义设置**以选择从预定义设置，或选择各个选项。 有关详细信息，请参阅[Driver Verifier 选项和规则类](driver-verifier-options.md)并[选择驱动程序验证工具选项](selecting-driver-verifier-options.md)。

3. 下**选择要验证哪些驱动程序**，选择以下表中所述的选择方案之一。

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">Option</th>
   <th align="left">建议的使用</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><strong>自动选择未签名驱动程序</strong></td>
   <td align="left"><p>可用于测试正在运行的不需要的 Windows 版本的计算机上已签名的驱动程序。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>自动选择内置较旧版本的 Windows 驱动程序</strong></td>
   <td align="left"><p>可用于测试与较新版本的 Windows 驱动程序兼容性。</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><strong>自动选择此计算机上安装的所有驱动程序</strong></td>
   <td align="left"><p>在系统上提供的驱动程序的测试数方面的最大覆盖范围。 此选项非常有用的其中一个驱动程序可以与其他设备或在系统上的驱动程序进行交互的测试方案。</p>
   <p>此选项还可耗尽的资源可供<a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊池</a>和跟踪某些资源。 测试所有驱动程序可能还会影响系统性能。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>从列表中选择驱动程序名称</strong></td>
   <td align="left"><p>在大多数情况下，你将想要指定要测试的驱动程序。</p>
   <p>选择设备堆栈中的所有驱动程序允许<a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">增强的 I/O 验证</a>选项来跟踪对象和检查符合性，因为每个堆栈，它允许更高版本中的驱动程序之间传递到 I/O 请求数据包 (IRP)要在检测到错误时提供的详细信息级别。</p>
   <p>选择单个驱动程序，如果您正在运行的测试方案的测量系统或驱动程序的性能指标，或如果你想要用于检测内存损坏或跟踪问题的资源分配最多的可用资源 (如死锁或互斥锁）。 <a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊池</a>并<a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/O 验证</a>选项是上一个驱动程序一次使用时更有效。</p></td>
   </tr>
   </tbody>
   </table>


4. 如果选择了**从列表中选择驱动程序名称**，单击**下一步**，然后选择一个或多个特定的驱动程序。

5. 单击**完成**，然后重启计算机。



>[!Note]
> 此外可以在命令提示符窗口中运行驱动程序验证程序，而无需启动驱动程序验证程序管理器。 例如，若要运行驱动程序验证程序的标准设置驱动程序上调用*myDriver.sys*，你可以使用以下命令：
> ```console
> verifier /standard /driver myDriver.sys
> ```
>
> 有关命令行选项的详细信息，请参阅[**驱动程序验证工具的命令语法**](verifier-command-line.md)。



## <a name="how-to-control-driver-verifier"></a>如何控制驱动程序验证程序

可以使用驱动程序验证程序管理器或命令行控制驱动程序验证程序。 若要启动驱动程序验证程序管理器，请参阅[如何启动驱动程序验证程序](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/driver-verifier#how-to-start-driver-verifier)本主题中前面部分。

对于每个以下的操作，可以使用驱动程序验证程序管理器或命令行输入。


**若要停止或重置 Driver Verifier**

1. 在中**驱动程序验证程序管理器**，选择**删除现有设置**，然后单击**完成**。

    或

    输入以下命令在命令提示符：

    ```console
    verifier /reset
    ```

2. 重新启动计算机。


**若要查看驱动程序验证程序统计信息**

- 在中**驱动程序验证程序管理器**，选择**显示有关当前已验证的驱动程序的信息**，然后单击**下一步**。 继续单击**下一步**显示的其他信息。

  或

  输入以下命令在命令提示符：

  ```console
  verifier /query
  ```


**若要查看驱动程序验证程序设置**

- 在中**驱动程序验证程序管理器**，选择**显示现有设置**，然后单击**下一步**。

  或

  输入以下命令在命令提示符：

  ```console
  verifier /querysettings
  ```


## <a name="how-to-debug-driver-verifier-violations"></a>如何调试驱动程序验证程序冲突

若要从驱动程序验证程序获得最佳效果，应使用内核调试程序并将其连接到测试计算机。 有关 Windows 调试工具的概述，请参阅[调试工具的 Windows （WinDbg、 KD、 CDB、 NTSD）](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/index)。

如果驱动程序验证程序检测到冲突，它将生成的 bug 检查停止计算机。 这是为了向您提供可能的大多数信息用于调试问题。 如果内核调试程序连接到正在运行驱动程序验证程序的测试计算机，并且驱动程序验证程序检测到冲突，Windows 进入调试器并显示错误的简短说明。

检测到的 bug 检查中的 Driver Verifier 结果的所有冲突。 常见的 bug 检查代码如下所示：

-   [**Bug 检查 0xC1:特殊\_池\_已检测\_内存\_损坏**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xc1--special-pool-detected-memory-corruption)
-   [**Bug 检查 0xC4:驱动程序\_VERIFIER\_检测到\_冲突**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)
-   [**Bug 检查为 0xC6:驱动程序\_CAUGHT\_修改\_FREED\_池**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xc6--driver-caught-modifying-freed-pool)
-   [**Bug 检查 0xC9:驱动程序\_VERIFIER\_IOMANAGER\_冲突**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xc9--driver-verifier-iomanager-violation)
-   [**Bug 检查 0xD6:驱动程序\_页上\_容错\_超出\_最终\_OF\_分配**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xd6--driver-page-fault-beyond-end-of-allocation)
-   [**Bug 检查 0xE6:驱动程序\_VERIFIER\_DMA\_冲突**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xe6--driver-verifier-dma-violation)

有关详细信息，请参阅[处理 Bug 检查时驱动程序验证程序已启用](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/handling-a-bug-check-when-driver-verifier-is-enabled)。 有关调试 Bug 检查 0xC4 的提示，请参阅[调试 Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突](debugging-bug-check-0xc4--driver-verifier-detected-violation.md)。

当你启动新的调试会话时，请使用调试器扩展命令， [ **！ 分析**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-analyze)。 在内核模式下 **！ 分析**命令显示有关最新的 bug 检查的信息。 若要显示*额外*信息，以帮助确定错误的驱动程序，将选项添加 **-v**到在执行命令**kd >** 提示符：

```dbgcmd
kd> !analyze -v
```

除了 **！ 分析**，可以输入在下面的调试器扩展**kd >** 提示若要查看特定于驱动程序验证程序的信息：

-   [**！ verifier** ](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-verifier)转储捕获驱动程序验证程序统计信息。 使用 **！ verifier-？** 若要显示所有可用的选项。

    ```dbgcmd
    kd> !verifier
    ```

-   [**！ 死锁**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-deadlock)显示与锁相关的信息或驱动程序验证程序的死锁检测功能跟踪对象。 使用 **！ 死锁的？** 若要显示所有可用的选项。

    ```dbgcmd
    kd> !deadlock
    ```

-   [**！ iovirp** ](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-iovirp) \[*地址*\]显示与跟踪的 I/O 验证程序 IRP 相关信息。 例如：

    ```dbgcmd
    kd> !iovirp 947cef68
    ```

-   [**！ ruleinfo** ](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-ruleinfo) \[ *RuleID* \]显示与相关信息[DDI 符合性检查](ddi-compliance-checking.md)所违反的规则。 (*RuleID*始终是 bug 检查的第一个参数。)所有规则 Id 从 DDI 符合性检查是否在窗体 0x200*nn*。 例如：

    ```dbgcmd
    kd> !ruleinfo 0x20005
    ```


## <a name="related-topics"></a>相关主题

[驱动程序验证程序：新增功能](driver-verifier--what-s-new.md)

[Driver Verifier 选项](driver-verifier-options.md)

[**驱动程序验证工具的命令语法**](verifier-command-line.md)

[使用驱动程序验证程序](using-driver-verifier.md)

[控制驱动程序验证程序](controlling-driver-verifier.md)
