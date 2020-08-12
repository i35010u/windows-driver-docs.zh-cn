---
title: Bug 检查 0x109 CRITICAL_STRUCTURE_CORRUPTION
description: CRITICAL_STRUCTURE_CORRUPTION bug 检查的值为0x00000109。 这表示内核检测到关键内核代码或数据损坏。
ms.assetid: 38d4d722-a915-4f17-899b-2a0b4aa69d95
keywords:
- Bug 检查 0x109 CRITICAL_STRUCTURE_CORRUPTION
- CRITICAL_STRUCTURE_CORRUPTION
ms.date: 05/13/2020
topic_type:
- apiref
api_name:
- CRITICAL_STRUCTURE_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d542d66e4338c4febcb82a217b5adb1c784bbabb
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148500"
---
# <a name="bug-check-0x109-critical_structure_corruption"></a>Bug 检查0x109：严重 \_ 结构 \_ 损坏


"关键 \_ 结构 \_ 损坏 bug 检查" 的值为 "0x00000109"。 这表示内核检测到关键内核代码或数据损坏。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅 [排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="critical_structure_corruption-parameters"></a>关键 \_ 结构 \_ 损坏参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>损坏区域的类型。  (在此页后面的部分中，请参阅下表。 ) </p></td>
</tr>
</tbody>
</table>

 

参数4的值指示已损坏区域的类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数4</th>
<th align="left">损坏的区域类型、损坏类型或导致损坏的操作类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>一般数据区域</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>函数修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>处理器中断调度表 (IDT) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>处理器全局描述符表 (GDT) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>类型1进程列表损坏</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>类型2进程列表损坏</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>调试例程修改</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>关键 MSR 修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>对象类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>处理器 IVT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xA</p></td>
<td align="left"><p>修改系统服务函数</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xB</p></td>
<td align="left"><p>一般会话数据区域</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xC</p></td>
<td align="left"><p>修改 session 函数或. pdata</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xD</p></td>
<td align="left"><p>修改导入表</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xE</p></td>
<td align="left"><p>修改会话导入表</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xF</p></td>
<td align="left"><p>Ps Win32 标注修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>调试切换例程修改</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x11</p></td>
<td align="left"><p>IRP 分配器修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x12</p></td>
<td align="left"><p>驱动程序调用调度程序修改</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x13</p></td>
<td align="left"><p>IRP 完成调度程序修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x14</p></td>
<td align="left"><p>IRP 释放器修改</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15</p></td>
<td align="left"><p>处理器控制寄存器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x16</p></td>
<td align="left"><p>关键浮点控件寄存器修改</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x17</p></td>
<td align="left"><p>本地 APIC 修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x18</p></td>
<td align="left"><p>内核通知标注修改</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x19</p></td>
<td align="left"><p>已加载模块列表修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1A</p></td>
<td align="left"><p>类型3进程列表损坏</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>类型4进程列表损坏</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1C</p></td>
<td align="left"><p>驱动程序对象损坏</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>执行回调对象修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>修改模块填充</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p>修改受保护的进程</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>一般数据区域</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>页面哈希不匹配</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>会话页面哈希不匹配</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>加载配置目录修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>反转函数表修改</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>会话配置修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>扩展处理器控制寄存器</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x27</p></td>
<td align="left"><p>类型1池损坏</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x28</p></td>
<td align="left"><p>类型2池损坏</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x29</p></td>
<td align="left"><p>类型3池损坏</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101</p></td>
<td align="left"><p>常规池损坏</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x102</p></td>
<td align="left"><p>修改 win32k.sys</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查通常有三个不同的原因：

1.  驱动程序无意或有意修改了关键内核代码或数据。 对于基于 x64 的计算机，Microsoft Windows Server 2003 Service Pack 1 (SP1) 和更高版本的 Windows 不允许对内核进行修补，除非已获得授权的 Microsoft 修补程序。

2.  开发人员试图使用系统启动时未连接的内核调试器来设置普通内核断点。 只有在启动时附加调试器，才能设置 ([**bp**](bp--bu--bm--set-breakpoint-.md)) 的常规断点。 可以随时设置 ([**ba**](ba--break-on-access-.md)) 的处理器断点。

3.  发生硬件损坏。 例如，内核代码或数据可能存储在失败的内存中。

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

若要开始，请使用 [**k、kb、glm-kc-qnw、kd、kp、kp、kv (显示 Stack Backtrace) **](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令来查看堆栈跟踪。 可以指定处理器编号来检查所有处理器上的堆栈。

你还可以在代码中设置一个断点，使其导致此 stop 代码，并尝试单步执行出错的代码。

有关详细信息，请参阅以下主题：

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

如果你不具备使用 Windows 调试器来处理此问题，则可以使用一些基本的故障排除技术。

-   查看事件查看器中的系统日志，以获取可能有助于识别导致此错误检查的设备或驱动程序的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   运行 Windows 内存诊断工具来测试内存。 在 "控制面板" 搜索框中键入 "内存"，然后单击 " **诊断计算机的内存问题**"。运行测试后，使用事件查看器查看系统日志下的结果。 查找 " *MemoryDiagnostics* " 项，查看结果。

-   你可以尝试运行系统制造商提供的硬件诊断。

-   确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如，可以在 [Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

-   有关其他常规疑难解答信息，请参阅 [**蓝屏数据**](blue-screen-data.md)。

 

 




