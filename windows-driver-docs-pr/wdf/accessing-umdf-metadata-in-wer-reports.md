---
title: 访问 WER 报表中的 UMDF 元数据
description: 本主题介绍的位置和用户模式驱动程序框架 (UMDF) 崩溃时操作系统会创建 Windows 错误报告 (WER) 报表的内容。系统会生成三种不同 UMDF 事件类型 WUDFHostProblem，WUDFUnhandledException，WER 报表和 WUDFVerifierFailure.When 反射器终止驱动程序主机进程中的，有时由于主机超时阈值被超出，系统会生成一个名为 Report.wer，其中包含 WER 信息文件。 具体而言，Report.wer 包含 UMDF 元数据可能会有所帮助，如果你尝试调试 UMDF 驱动程序不能访问到实时调试目标。
ms.assetid: ca5fe108-b4fb-4c90-87bc-9901854780d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b2832acc46db365c425315e4b92f6dcdd51d6dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568606"
---
# <a name="accessing-umdf-metadata-in-wer-reports"></a>访问 WER 报表中的 UMDF 元数据


本主题介绍的位置和用户模式驱动程序框架 (UMDF) 崩溃时操作系统会创建 Windows 错误报告 (WER) 报表的内容。

系统会生成 WER 报表以了解三个不同的 UMDF 事件类型：**WUDFHostProblem**， **WUDFUnhandledException**，和**WUDFVerifierFailure**。

当该发送程序终止时驱动程序主机进程中，有时由于[主机超时](how-umdf-enforces-time-outs.md)阈值被超出，系统将生成一个名为 Report.wer，其中包含 WER 信息文件。 具体而言，Report.wer 包含 UMDF 元数据可能会有所帮助，如果你尝试调试 UMDF 驱动程序不能访问到实时调试目标。

在 Windows 8.1 中可以找到 Report.wer 文件，在 c:\\ProgramData\\Microsoft\\Windows\\WER\\ReportQueue 目录。 在此目录中打开最新的非关键性\_HostProblem\_ \*文件夹并找到 Report.wer。

您还可以访问使用以下 PowerShell 命令的 UMDF WER 报表：

```cpp
get-winevent -providername "Windows Error Reporting" | where-object {$_.Message -like "*wudf*"} | format-list | out-file UmdfReports.txt
```

## <a name="wudfhostproblem-sample-report"></a>WUDFHostProblem 示例报表


下面是示例类型的 UMDF WER 报表**WUDFHostProblem**。 获取从上面所述的 ReportQueue 目录了。 如果使用 PowerShell 来检索报表，可以标记字段而不是 Sig P0，P1，P2\[0\]，Sig\[1\]，Sig\[2\]。 否则为字段是相同的并且包含相同的可能值。 此示例是从使用 OSR USB FX2 硬件参考板的 WDK 示例之一生成的。

```cpp
Sig[0].Name=EventClass
Sig[0].Value=HostProblem
Sig[1].Name=Problem
Sig[1].Value=HostTimeout
Sig[2].Name=DetectedBy
Sig[2].Value=2
Sig[3].Name=UMDFVersion
Sig[3].Value=6.3.9600
Sig[4].Name=ExitCode
Sig[4].Value=103
Sig[5].Name=Operation
Sig[5].Value=3
Sig[6].Name=Message
Sig[6].Value=11b00
Sig[7].Name=Status
Sig[7].Value=ffffffff
Sig[8].Name=HardwareId
Sig[8].Value=USB\VID_0547&PID_1002&REV_0000
```

## <a name="wudfhostproblem-fields"></a>WUDFHostProblem 字段


下表描述了类型的报表中的字段的可能值**WUDFHostProblem。**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引</th>
<th align="left">“属性”</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">EventClass</td>
<td align="left"><p>该框架将此值设置为<strong>HostProblem</strong>。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">问题</td>
<td align="left"><p>此字段包含以下值之一：</p>
<ul>
<li>HostFailure</li>
<li>SendFailure</li>
<li>HostTimeout</li>
<li>BadRequest</li>
<li>BadReply</li>
<li>HostFailure</li>
<li>其他</li>
<li>HostDisconnect</li>
<li>LeakedHandle</li>
<li>InvalidInterruptState</li>
<li>IsrTimedOut</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">DetectedBy</td>
<td align="left"><p>包含下列枚举值之一：</p>
<div class="code">
<code>cpp
WdfComponentInvalid = 0,
WdfComponentPlatform,
WdfComponentReflector,
WdfComponentDriverManager,
WdfComponentHost,
WdfComponentFramework,
WdfComponentTest,
WdfComponentMax</code>
</div></td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">UMDFVersion</td>
<td align="left"><p>指定当前正在使用 UMDF 库的版本。 如果用户采取操作以更新框架库，请注意，这可能是更高版本比随操作系统一起提供。</p></td>
</tr>
<tr class="odd">
<td align="left">4</td>
<td align="left">ExitCode</td>
<td align="left"><p>包含下列枚举值之一：</p>
<div class="code">
<code>cpp
    WdfHostExit_StillActive = 0x103,
    WdfHostExit_CodeUnknown = 0x70000000,
    WdfHostExit_InternalDriverStopReported,
    WdfHostExit_InternalDriverStopReportFailed,
    WdfHostExit_ExternalTermination</code>
</div>
<p><strong>WdfHostExit_StillActive</strong>指示主机进程已运行时框架创建错误报告。</p></td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">操作</td>
<td align="left"><p>包含下列枚举值之一：</p>
<div class="code">
<code>cpp
    WudfOperation_Invalid,
    WudfOperation_Init,
    WudfOperation_HostShutdown,
    WudfOperation_Pnp,
    WudfOperation_Cleanup,
    WudfOperation_Close,
    WudfOperation_Cancel,
    WudfOperation_IO,
    WudfOperation_Interrupt,
    WudfOperation_PoFx,
    WudfOperation_Other,
    WudfOperation_Max</code>
</div></td>
</tr>
<tr class="odd">
<td align="left">6</td>
<td align="left">消息</td>
<td align="left"><p>第一个数字是此字段将始终为 1，指示 IRP 参与该操作。 后续对的数字表示指示<strong>MajorFunction</strong>并<strong>MinorFunction</strong>的 IRP，分别。</p>
<p>例如，在上述示例报表中，此字段包含值 11b00。 这意味着的操作是 IRP 反射器处理代表 IRP_MJ_PNP 主要函数值，并执行了 IRP_MN_START_DEVICE 次要函数值与驱动程序主机进程 (1 = IRP 消息，1b = IRP_MJ_PNP，00 = 执行了 IRP_MN_START_DEVICE)。</p></td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">状态</td>
<td align="left"><p>框架将始终设置为此值为 0xffffffff。</p></td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">HardwareId</td>
<td align="left"><p>此字段包含遇到的问题的驱动程序与关联的设备的硬件 ID。</p></td>
</tr>
</tbody>
</table>



## <a name="wudfunhandledexception-fields"></a>WUDFUnhandledException 字段


下表描述了类型的报表中的字段的可能值**WUDFUnhandledException**。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引</th>
<th align="left">“属性”</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">EventClass</td>
<td align="left"><p>该框架将此值设置为<strong>UnhandledException</strong>。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">组件</td>
<td align="left"><p>此字段包含以下值之一：</p>
<ul>
<li>无效</li>
<li>平台</li>
<li>反射器</li>
<li>DriverManager</li>
<li>主机</li>
<li>框架</li>
<li>测试</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">ExceptionCode</td>
<td align="left"><p>发生异常的原因。 值的列表，请参阅<a href="https://msdn.microsoft.com/library/windows/desktop/aa363082" data-raw-source="[&lt;strong&gt;EXCEPTION_RECORD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363082)"> <strong>EXCEPTION_RECORD</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">RelativeFaultingAddress</td>
<td align="left"><p>异常发生位置的地址。</p></td>
</tr>
<tr class="odd">
<td align="left">4</td>
<td align="left">CrashingModuleName</td>
<td align="left">引发异常的驱动程序的名称。</td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">CrashingFileVersion</td>
<td align="left">Framework 版本的驱动程序。</td>
</tr>
<tr class="odd">
<td align="left">6</td>
<td align="left">LastDriverName</td>
<td align="left">驱动程序堆栈中的第一个非 UMDF 驱动程序组件的名称。</td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">LastDriverVersion</td>
<td align="left">驱动程序堆栈中的第一个非 UMDF 驱动程序组件的版本号。</td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">UMDFVersion</td>
<td align="left"><p>指定当前正在使用 UMDF 库的版本。 如果用户采取操作以更新框架库，请注意，这可能是更高版本比随操作系统一起提供。</p></td>
</tr>
<tr class="even">
<td align="left">9</td>
<td align="left">HardwareId</td>
<td align="left"><p>从 Windows 8 开始，在单独的文件中提供的硬件 ID。 在这种情况下，框架将此值设置为<strong>单独转储</strong>。</p></td>
</tr>
</tbody>
</table>



## <a name="wudfverifierfailure-fields"></a>WUDFVerifierFailure 字段


下表描述了类型的报表中的字段的可能值**WUDFVerifierFailure**。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引</th>
<th align="left">“属性”</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">EventClass</td>
<td align="left"><p>该框架将此值设置为<strong>VerifierFailure</strong>。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">FoundBy</td>
<td align="left"><p>该框架将此值设置为<strong>Framework</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">类别</td>
<td align="left"><p>此字段包含以下值之一：</p>
<ul>
<li>内部</li>
<li>驱动程序</li>
<li>调用方</li>
<li>外部</li>
<li>UnhandledException</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">ErrorNumber</td>
<td align="left">仅限内部使用。</td>
</tr>
<tr class="odd">
<td align="left">4</td>
<td align="left">位置</td>
<td align="left">仅限内部使用。</td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">驱动程序</td>
<td align="left">失败的驱动程序模块的名称。</td>
</tr>
<tr class="odd">
<td align="left">6</td>
<td align="left">CallerAddress</td>
<td align="left">启动生成报表的例程的地址。</td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">UMDFVersion</td>
<td align="left"><p>指定当前正在使用 UMDF 库的版本。 如果用户采取操作以更新框架库，请注意，这可能是更高版本比随操作系统一起提供。</p></td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">HardwareId</td>
<td align="left"><p>从 Windows 8 开始，在单独的文件中提供的硬件 ID。 在这种情况下，框架将此值设置为<strong>单独转储</strong>。</p></td>
</tr>
</tbody>
</table>











