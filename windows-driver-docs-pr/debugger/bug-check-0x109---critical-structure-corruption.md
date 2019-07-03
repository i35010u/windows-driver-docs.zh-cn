---
title: Bug 检查 0x109 CRITICAL_STRUCTURE_CORRUPTION
description: CRITICAL_STRUCTURE_CORRUPTION bug 检查具有 0x00000109 值。 这表示在内核检测到关键内核代码或数据损坏。
ms.assetid: 38d4d722-a915-4f17-899b-2a0b4aa69d95
keywords:
- Bug 检查 0x109 CRITICAL_STRUCTURE_CORRUPTION
- CRITICAL_STRUCTURE_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CRITICAL_STRUCTURE_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 92ed8c35d1fbe2ebfcb6bc451296cea3c5b9362a
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521425"
---
# <a name="bug-check-0x109-criticalstructurecorruption"></a>Bug 检查 0x109：关键\_结构\_损坏


严重\_结构\_损坏错误检查的值为 0x00000109。 这表示在内核检测到关键内核代码或数据损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="criticalstructurecorruption-parameters"></a>关键\_结构\_损坏参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
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
<td align="left"><p>损坏区域的类型。 （请参阅下表更高版本在此页。）</p></td>
</tr>
</tbody>
</table>

 

参数 4 的值指示的损坏区域的类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 4</th>
<th align="left">类型的损坏的区域、 损坏，类型或类型执行的操作导致损坏</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>通用数据区域</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>函数修改或基于 Itanium 的函数位置</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>处理器中断分配表 (IDT)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>处理器全局描述符表 (GDT)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>类型 1 进程列表损坏</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>类型 2 进程列表损坏</p></td>
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
<td align="left"><p>处理器程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xA</p></td>
<td align="left"><p>修改的系统服务函数</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xB</p></td>
<td align="left"><p>泛型会话数据区域</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xC</p></td>
<td align="left"><p>会话函数或.pdata 的修改</p></td>
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
<td align="left"><p>调试开关例程修改</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x11</p></td>
<td align="left"><p>IRP 的分配器修改</p></td>
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
<td align="left"><p>IRP 的释放函数修改</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15</p></td>
<td align="left"><p>一个处理器控制寄存器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x16</p></td>
<td align="left"><p>浮动点控制寄存器修改严重</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x17</p></td>
<td align="left"><p>本地 APIC 修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x18</p></td>
<td align="left"><p>内核标注修改通知</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x19</p></td>
<td align="left"><p>加载的模块列表修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1A</p></td>
<td align="left"><p>类型 3 进程列表损坏</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>类型 4 进程列表损坏</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1C</p></td>
<td align="left"><p>驱动程序对象损坏</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>执行回调对象的修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>修改的模块填充</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p>受保护的进程的修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>通用数据区域</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>页哈希不匹配</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>会话页哈希不匹配</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>加载配置目录修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>倒排的函数表修改</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>会话配置修改</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>扩展的处理器控制寄存器</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x27</p></td>
<td align="left"><p>键入 1 池损坏</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x28</p></td>
<td align="left"><p>类型为 2 池损坏</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x29</p></td>
<td align="left"><p>类型 3 池损坏</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101</p></td>
<td align="left"><p>常规池损坏</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x102</p></td>
<td align="left"><p>Win32k.sys 的修改</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

通常有三个不同的原因导致此错误检查：

1.  驱动程序的无意中，或故意，关键内核代码或数据修改。 Microsoft Windows Server 2003 Service Pack 1 (SP1) 和更高版本的 Windows 基于 x64 的计算机不允许通过已授权 Microsoft 发起的热修补程序，除要修补的内核。 有关详细信息，请参阅[针对基于 x64 的系统的修补策略](https://go.microsoft.com/fwlink/p/?linkid=50719)。

2.  开发人员尝试正常内核使用设置断点时系统启动时未附加内核调试程序。 普通断点 ([**bp**](bp--bu--bm--set-breakpoint-.md)) 只能如果调试器已附加的开始时间设置。 处理器断点 ([**ba**](ba--break-on-access-.md)) 可以在任何时间设置。

3.  出现硬件损坏。 例如，内核代码或数据可能已存储在内存中失败。

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

若要开始，请检查堆栈跟踪使用[ **k、 kb、 kc、 kd、 kp、 kP，kv （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令。 您可以指定要检查堆栈上的所有处理器的处理器数。

此外可以导致此停止代码在代码中设置断点并单步前进到出错的代码尝试。

有关详细信息，请参阅以下主题：

[故障转储分析使用 Windows 调试器 (WinDbg)](crash-dump-files.md)

如果您不准备使用 Windows 调试器处理此问题，可以使用一些基本的故障排除方法。

-   检查事件查看器中的系统日志可能有助于识别设备或驱动程序导致此错误检查的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   运行 Windows 内存诊断工具，用于测试的内存。 在控件面板的搜索框中，键入内存，然后单击**诊断您的计算机的内存问题**。在测试运行后，使用事件查看器查看系统日志下的结果。 寻找*MemoryDiagnostics 结果*条目以查看结果。

-   您可以尝试运行硬件诊断程序提供的系统制造商。

-   确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

 

 




