---
title: 访问 WER 报表中的 UMDF 元数据
description: 本主题介绍在用户模式驱动程序框架（UMDF）崩溃时操作系统创建的 Windows 错误报告（WER）报告的位置和内容。系统会为 WUDFHostProblem、WUDFUnhandledException 和 WUDFVerifierFailure 三个不同的 UMDF 事件类型生成 WER 报告。当反射器终止驱动程序主机进程时，有时是由于超过了主机超时阈值，系统会生成一个名为的文件，其中包含 WER 信息。 具体而言，如果您尝试在没有访问实时调试目标的情况下调试 UMDF 驱动程序，则 wer 包含 UMDF 元数据可能会很有帮助。
ms.assetid: ca5fe108-b4fb-4c90-87bc-9901854780d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34a408d946d540a6011e33d0341b92b06b4b0a3c
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210231"
---
# <a name="accessing-umdf-metadata-in-wer-reports"></a>访问 WER 报表中的 UMDF 元数据


本主题介绍在用户模式驱动程序框架（UMDF）崩溃时操作系统创建的 Windows 错误报告（WER）报告的位置和内容。

系统会为三种不同的 UMDF 事件类型生成 WER 报告： **WUDFHostProblem**、 **WUDFUnhandledException**和**WUDFVerifierFailure**。

当反射器终止驱动程序主机进程时，有时由于超过了[主机超时](how-umdf-enforces-time-outs.md)阈值，系统将生成一个名为 "node.js" 的文件，其中包含 wer 信息。 具体而言，如果您尝试在没有访问实时调试目标的情况下调试 UMDF 驱动程序，则 wer 包含 UMDF 元数据可能会很有帮助。

在 Windows 8.1 中，可以在 C：\\ProgramData\\Microsoft\\Windows\\WER\\ReportQueue 目录中找到文件。 在此目录中，打开最新的非关键性\_HostProblem\_\* 文件夹，并找到 "wer"。

你还可以使用以下 PowerShell 命令访问适用于 UMDF 的 WER 报告：

```cpp
get-winevent -providername "Windows Error Reporting" | where-object {$_.Message -like "*wudf*"} | format-list | out-file UmdfReports.txt
```

## <a name="wudfhostproblem-sample-report"></a>WUDFHostProblem 示例报表


下面是**WUDFHostProblem**类型的示例 UMDF WER 报告。 它是从上面所述的 ReportQueue 目录中获得的。 如果使用 PowerShell 检索报表，则字段可能标记为 P0、P1、P2，而不是 Sig\[0\]、Sig\[1\]、Sig\[2\]。 否则，这些字段是相同的，并包含相同的可能值。 此示例是通过使用 OSR USB-FX2 硬件参考板的某个 WDK 示例生成的。

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


下表描述了 WUDFHostProblem 类型的报表中字段的可能值 **。**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引</th>
<th align="left">名称</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">EventClass</td>
<td align="left"><p>框架将此值设置为<strong>HostProblem</strong>。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">问题</td>
<td align="left"><p>此字段包含下列值之一：</p>
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
<td align="left"><p>包含以下枚举值之一：</p>
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
<td align="left"><p>指定当前使用的 UMDF 库的版本。 请注意，如果用户采取操作更新框架库，此版本可能比操作系统附带的版本更高。</p></td>
</tr>
<tr class="odd">
<td align="left">4</td>
<td align="left">ExitCode</td>
<td align="left"><p>包含以下枚举值之一：</p>
<div class="code">
<code>cpp
    WdfHostExit_StillActive = 0x103,
    WdfHostExit_CodeUnknown = 0x70000000,
    WdfHostExit_InternalDriverStopReported,
    WdfHostExit_InternalDriverStopReportFailed,
    WdfHostExit_ExternalTermination</code>
</div>
<p><strong>WdfHostExit_StillActive</strong>指示在框架创建错误报告时主机进程正在运行。</p></td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">操作</td>
<td align="left"><p>包含以下枚举值之一：</p>
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
<td align="left"><p>此字段的第一个数字始终为1，指示操作涉及 IRP。 后续位数分别指示 IRP 的<strong>MajorFunction</strong>和<strong>MinorFunction</strong> 。</p>
<p>例如，在上面的示例报表中，此字段包含值11b00。 这意味着该操作是一个 IRP，反映器代表驱动程序主机进程处理，其主要函数值为 IRP_MJ_PNP，次函数值为 IRP_MN_START_DEVICE （1 = IRP message，1b = IRP_MJ_PNP，00 = IRP_MN_START_DEVICE）。</p></td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">状态</td>
<td align="left"><p>框架始终将此值设置为0xffffffff。</p></td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">HardwareId</td>
<td align="left"><p>此字段包含与存在问题的驱动程序相关联的设备的硬件 ID。</p></td>
</tr>
</tbody>
</table>



## <a name="wudfunhandledexception-fields"></a>WUDFUnhandledException 字段


下表描述了**WUDFUnhandledException**类型的报表中字段的可能值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引</th>
<th align="left">名称</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">EventClass</td>
<td align="left"><p>框架将此值设置为<strong>UnhandledException</strong>。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">Component</td>
<td align="left"><p>此字段包含下列值之一：</p>
<ul>
<li>无效</li>
<li>平台</li>
<li>反映</li>
<li>DriverManager</li>
<li>Host</li>
<li>框架</li>
<li>测试</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">ExceptionCode</td>
<td align="left"><p>异常发生的原因。 有关值的列表，请参阅<a href="https://docs.microsoft.com/windows/win32/api/winnt/ns-winnt-exception_record" data-raw-source="[&lt;strong&gt;EXCEPTION_RECORD&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winnt/ns-winnt-exception_record)"><strong>EXCEPTION_RECORD</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">RelativeFaultingAddress</td>
<td align="left"><p>发生异常的地址。</p></td>
</tr>
<tr class="odd">
<td align="left">4</td>
<td align="left">CrashingModuleName</td>
<td align="left">引发异常的驱动程序的名称。</td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">CrashingFileVersion</td>
<td align="left">驱动程序的框架版本。</td>
</tr>
<tr class="odd">
<td align="left">6</td>
<td align="left">LastDriverName</td>
<td align="left">驱动程序堆栈中第一个非 UMDF 驱动程序组件的名称。</td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">LastDriverVersion</td>
<td align="left">驱动程序堆栈中第一个非 UMDF 驱动程序组件的版本号。</td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">UMDFVersion</td>
<td align="left"><p>指定当前使用的 UMDF 库的版本。 请注意，如果用户采取操作更新框架库，此版本可能比操作系统附带的版本更高。</p></td>
</tr>
<tr class="even">
<td align="left">9</td>
<td align="left">HardwareId</td>
<td align="left"><p>从 Windows 8 开始，将在单独的文件中提供硬件 ID。 在这种情况下，框架会将此值设置为<strong>单独转储</strong>。</p></td>
</tr>
</tbody>
</table>



## <a name="wudfverifierfailure-fields"></a>WUDFVerifierFailure 字段


下表描述了**WUDFVerifierFailure**类型的报表中字段的可能值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引</th>
<th align="left">名称</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">EventClass</td>
<td align="left"><p>框架将此值设置为<strong>VerifierFailure</strong>。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">FoundBy</td>
<td align="left"><p>框架将此值设置为<strong>framework</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">类别</td>
<td align="left"><p>此字段包含下列值之一：</p>
<ul>
<li>内置</li>
<li>“驱动程序”</li>
<li>Caller</li>
<li>外部</li>
<li>UnhandledException</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">错误号</td>
<td align="left">仅限内部使用。</td>
</tr>
<tr class="odd">
<td align="left">4</td>
<td align="left">位置</td>
<td align="left">仅限内部使用。</td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">“驱动程序”</td>
<td align="left">失败的驱动程序模块的名称。</td>
</tr>
<tr class="odd">
<td align="left">6</td>
<td align="left">CallerAddress</td>
<td align="left">发起报表生成的例程的地址。</td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">UMDFVersion</td>
<td align="left"><p>指定当前使用的 UMDF 库的版本。 请注意，如果用户采取操作更新框架库，此版本可能比操作系统附带的版本更高。</p></td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">HardwareId</td>
<td align="left"><p>从 Windows 8 开始，将在单独的文件中提供硬件 ID。 在这种情况下，框架会将此值设置为<strong>单独转储</strong>。</p></td>
</tr>
</tbody>
</table>











