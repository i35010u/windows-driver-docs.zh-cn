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
ms.openlocfilehash: 9f91dca761d53253a8bcf301851ad2a5a7aa404d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521607"
---
# <a name="driver-verifier"></a>驱动程序验证程序


驱动程序验证工具可监视 Windows 内核模式驱动程序和图形驱动程序以检测非法的函数调用或可能会损坏系统的操作。 驱动程序验证程序可以使用者到各种压力和测试，以找到不正确的行为的 Windows 驱动程序。

您可以驱动程序验证程序上运行多个驱动程序同时，或一个驱动程序上一次。 你可以配置哪些测试运行，这使你可以通过超负荷加载或更多简化测试放置一个驱动程序。

-   [在何处可以下载驱动程序验证程序](#where-can-i-download-driver-verifier)
-   [何时使用 Driver Verifier](#when-to-use-driver-verifier)
-   [如何启动驱动程序验证程序](#how-to-start-driver-verifier)
-   [如何控制驱动程序验证程序](#how-to-control-driver-verifier)
-   [如何调试驱动程序验证程序冲突](#how-to-debug-driver-verifier-violations)
-   [相关的主题](#related-topics)



## <a name="where-can-i-download-driver-verifier"></a>在何处可以下载驱动程序验证程序


<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>您不&#39;无需下载驱动程序验证程序 (Verifier.exe)，因为 Windows 2000，除 Windows 10 s。 之后，每个版本的 Windows 中包含没有&#39;t 单独的驱动程序验证程序下载包，它位于 %windir%\system32 目录中。 </p>
<ul>
<li>打开<strong>命令提示符</strong>窗口 (<strong>以管理员身份运行</strong>)。</li>
<li>类型<strong>verifier</strong>以打开驱动程序验证程序管理器，或类型<strong>verifier /？</strong> 若要查看命令行选项。 请参阅<a href="verifier-command-line.md" data-raw-source="[&lt;strong&gt;Driver Verifier Command Syntax&lt;/strong&gt;](verifier-command-line.md)"><strong>驱动程序验证工具的命令语法</strong></a>有关详细信息。</li>
</ul>
<p></p>
<div class="alert">
<strong>警告</strong><br/><ul>
<li>运行驱动程序验证程序可能会导致计算机崩溃。</li>
<li>您只应将用于测试和调试的计算机上运行驱动程序验证程序。</li>
<li>您必须在计算机上 Administrators 组，使用驱动程序验证程序中。</li>
<li>驱动程序验证程序不包含在 Windows 10 s。我们建议改为在 Windows 10 中测试驱动程序行为。</li>
</ul>
</div>
<div>

</div>
<p>有关 Windows 8.1 驱动程序版本和以前版本的 Windows 中的更改的信息，请参阅<a href="driver-verifier--what-s-new.md" data-raw-source="[Driver Verifier: What&#39;s New](driver-verifier--what-s-new.md)">Driver Verifier:什么&#39;新增</a>。</p></td>
</tr>
</tbody>
</table>





## <a name="when-to-use-driver-verifier"></a>何时使用 Driver Verifier


驱动程序开发过程中运行 Driver Verifier 和测试过程。

-   使用 Driver Verifier 早期阶段发现问题时更加容易，不在开发生命周期成本高昂，若要更正。

-   在部署用于测试使用 WDK，Visual Studio 中，驱动程序时使用驱动程序验证程序和[Windows 硬件认证工具包](https://go.microsoft.com/fwlink/p/?linkid=254893)(HCK) 测试。 请参阅[测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver)。

-   使用驱动程序验证程序进行故障排除和调试测试失败和计算机崩溃。



## <a name="how-to-start-driver-verifier"></a>如何启动驱动程序验证程序


只应在测试计算机或计算机是测试和调试运行驱动程序验证程序。 若要从驱动程序验证程序获得最佳效果，应使用内核调试程序并连接到测试计算机。 请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。

1. 打开**命令提示符**窗口 (**以管理员身份运行**) 和类型**verifier**打开驱动程序验证程序管理器。
2. 选择**创建标准设置**（默认值），单击**下一步**。

   你还可以选择**创建自定义设置**以选择从预定义设置，或选择各个选项。 请参阅[Driver Verifier 选项](driver-verifier-options.md)并[选择驱动程序验证工具选项](selecting-driver-verifier-options.md)有关详细信息。

3. 选择驱动程序或驱动程序验证。

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">选项</th>
   <th align="left">建议的使用</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><strong>自动选择未签名驱动程序</strong></td>
   <td align="left"><p>测试运行的 Windows 完全版本的计算机上的有用选项&#39;t 需要签名的驱动程序。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>自动选择内置较旧版本的 Windows 驱动程序</strong></td>
   <td align="left"><p>测试与较新版本的 Windows 驱动程序兼容性的有用选项。</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><strong>自动选择此计算机上安装的所有驱动程序</strong></td>
   <td align="left"><p>在系统上提供的驱动程序的测试数方面的最大覆盖范围。 此选项非常有用的其中一个驱动程序可以与其他设备或在系统上的驱动程序进行交互的测试方案。</p>
   <p>此选项还可耗尽的资源可供<a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊池</a>和跟踪某些资源。 测试所有驱动程序可能还会影响系统性能。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>从列表中选择驱动程序名称</strong></td>
   <td align="left"><p>在大多数情况下，你将想要指定要测试的驱动程序。</p>
   <p>选择设备堆栈中的所有驱动程序允许<a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">增强的 I/O 验证</a>选项来跟踪对象和 IRP 每个堆栈中的驱动程序之间传递，并允许更详细地提供检查符合性如果找到错误。</p>
   <p>如果您正在运行的测试方案的测量系统或驱动程序的性能指标，或如果你想要用于检测内存损坏或资源跟踪问题 （死锁、 mutexs） 分配最多的可用资源，请选择单个驱动程序。 <a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊池</a>并<a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/O 验证</a>选项会在一个驱动程序上一次使用时更有效。</p></td>
   </tr>
   </tbody>
   </table>



4. 单击**完成**和重新启动计算机。

**请注意**还可以在命令提示符窗口中运行驱动程序验证程序。 例如，若要运行驱动程序验证程序的标准设置名为 myDriver.sys 的驱动程序，将使用以下命令：



```
verifier  /standard /driver myDriver.sys
```

请参阅[**驱动程序验证工具的命令语法**](verifier-command-line.md)有关详细信息。



## <a name="how-to-control-driver-verifier"></a>如何控制驱动程序验证程序


**若要停止或重置 Driver Verifier**

1.  打开**命令提示符**窗口 (**以管理员身份运行**) 和类型**verifier**打开驱动程序验证程序管理器。
2.  选择**删除现有设置**。
3.  重新启动计算机。

或在命令提示符窗口中键入以下命令并重新启动计算机。

```
verifier  /reset
```

**若要查看驱动程序验证程序设置**

1.  打开**命令提示符**窗口 (**以管理员身份运行**) 和类型**verifier**打开驱动程序验证程序管理器。
2.  选择**显示现有设置**。

或在命令提示符窗口中键入以下命令。

```
verifier  /querysettings
```

**若要查看驱动程序验证程序统计信息**

1.  打开**命令提示符**窗口 (**以管理员身份运行**) 和类型**verifier**打开驱动程序验证程序管理器。
2.  选择**显示有关当前已验证的驱动程序信息**。

或在命令提示符窗口中键入以下命令。

```
verifier  /query
```



## <a name="how-to-debug-driver-verifier-violations"></a>如何调试驱动程序验证程序冲突


若要从驱动程序验证程序获得最佳效果，应使用内核调试程序并连接到测试计算机。 请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)有关详细信息。

如果驱动程序验证程序检测到冲突，它将生成的 bug 检查停止计算机。 这是为了向您提供可能的大多数信息用于调试问题。 内核调试程序连接到测试计算机运行驱动程序验证程序，如果驱动程序验证程序检测到冲突后，Windows 将进入调试器并显示错误的简短说明。

所有驱动程序验证程序冲突导致错误检查，最常见的 （尽管不一定是所有这些） 是：

-   [**Bug 检查 0xC1:特殊\_池\_已检测\_内存\_损坏**](https://msdn.microsoft.com/library/windows/hardware/ff560183)
-   [**Bug 检查 0xC4:驱动程序\_VERIFIER\_检测到\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187)
-   [**Bug 检查为 0xC6:驱动程序\_CAUGHT\_修改\_FREED\_池**](https://msdn.microsoft.com/library/windows/hardware/ff560193)
-   [**Bug 检查 0xC9:驱动程序\_VERIFIER\_IOMANAGER\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560205)
-   [**Bug 检查 0xD6:驱动程序\_页上\_容错\_超出\_最终\_OF\_分配**](https://msdn.microsoft.com/library/windows/hardware/ff560267)
-   [**Bug 检查 0xE6:驱动程序\_VERIFIER\_DMA\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560341)

有关详细信息请参阅[处理 Bug 检查时驱动程序验证程序已启用](https://msdn.microsoft.com/library/windows/hardware/hh450984)。 有关调试 Bug 检查 0xC4 的提示，请参阅[调试 Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突](debugging-bug-check-0xc4--driver-verifier-detected-violation.md)。

当你启动新的调试会话时，请使用调试器扩展命令[ **！ 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112)。 在内核模式下 **！ 分析**命令显示有关最新的 bug 检查的信息。 **！ 分析-v**命令显示的其他信息，并尝试找出错误的驱动程序。

```
kd> !analyze -v
```

此外[ **！ 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112)，可以使用以下调试器扩展来查看特定于驱动程序验证程序的信息：

-   [**！ verifier** ](https://msdn.microsoft.com/library/windows/hardware/ff565591)转储捕获驱动程序验证程序统计信息。 使用 **！ verifier-？** 若要显示所有可用的选项。

    ```
    kd> !verifier
    ```

-   [**！ 死锁**](https://msdn.microsoft.com/library/windows/hardware/ff562326)显示与锁相关的信息或驱动程序验证程序的死锁检测功能跟踪对象。 使用 **！ 死锁的？** 若要显示所有可用的选项。

    ```
    kd> !deadlock
    ```

-   [**！ iovirp** ](https://msdn.microsoft.com/library/windows/hardware/ff563252) \[*地址*\]显示与跟踪的 I/O 验证程序 IRP 相关信息。 例如：

    ```
    kd> !iovirp 947cef68
    ```

-   [**！ ruleinfo** ](https://msdn.microsoft.com/library/windows/hardware/dn265374) \[ *RuleID* \]显示与相关信息[DDI 符合性检查](ddi-compliance-checking.md)所违反的规则 (*RuleID*始终是 bug 检查的第一个参数。 所有 DDI 符合性检查*RuleID*窗体 0x200nn 中)。 例如：

    ```
    kd> !ruleinfo 0x20005
    ```



## <a name="related-topics"></a>相关主题


[驱动程序验证程序：新增功能](driver-verifier--what-s-new.md)

[Driver Verifier 选项](driver-verifier-options.md)

[**驱动程序验证工具的命令语法**](verifier-command-line.md)

[使用驱动程序验证程序](using-driver-verifier.md)

[控制驱动程序验证程序](controlling-driver-verifier.md)










