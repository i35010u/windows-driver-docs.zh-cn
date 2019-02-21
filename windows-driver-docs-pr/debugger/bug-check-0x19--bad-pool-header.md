---
title: Bug 检查 0x19 BAD_POOL_HEADER
description: BAD_POOL_HEADER bug 检查具有 0x00000019 值。 这表示池标头已损坏。
ms.assetid: a3e84703-d778-426b-80e6-e143f5d8f869
keywords:
- （开发人员内容）Bug 检查 0x19 BAD_POOL_HEADER
- BAD_POOL_HEADER
ms.date: 12/07/2017
topic_type:
- apiref
api_name:
- BAD_POOL_HEADER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4b8dff91de6527a79daf8f40c2481507cfd451a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526362"
---
# <a name="developer-content-bug-check-0x19-badpoolheader"></a>（开发人员内容）Bug 检查 0x19:错误\_池\_标头


缺点\_池\_标头错误检查的值为 0x00000019。 这表示池标头已损坏。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="badpoolheader-parameters"></a>错误\_池\_标头参数


参数 1 指示冲突的类型。 其他参数的含义取决于参数 1 的值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>正在检查池项</p></td>
<td align="left"><p>池块的大小</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>特殊池模式检查失败。</p>
<p>（所有者可能损坏了池块。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>正在检查池项</p></td>
<td align="left"><p>读回<strong>flink</strong> freelist 值</p></td>
<td align="left"><p>读回<strong>闪烁</strong>freelist 值</p></td>
<td align="left"><p>池空闲列表已损坏。</p>
<p>（在正常的列表中，参数 2、 3 和 4 的值应相同。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>一个池条目</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>其他池项</p></td>
<td align="left"><p>一对相邻池条目具有相互的标头。 在至少一个已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>错误地计算的一个条目</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>错误导致错误的计算的入口</p></td>
<td align="left"><p>池块标头&#39;s 以前大小来说太大。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>错误池项</p></td>
<td align="left"><p>池块标头大小已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>错误池项</p></td>
<td align="left"><p>池块标头大小为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>错误地计算的一个条目</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>错误导致错误的计算的入口</p></td>
<td align="left"><p>池块标头大小已损坏 （它是太大）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xA</p></td>
<td align="left"><p>应找到池项</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>应该包含池项页的虚拟地址</p></td>
<td align="left"><p>池块标头大小已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xD、 0xE，0xF、 0x23，0x24，0x25</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>已释放后已修改已释放的块的池标头。 这通常不是块的之前所有者释放; 的故障而是它通常是 （但不是总是） 由于前面超限释放的块的块。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>应找到池项</p></td>
<td align="left"><p>下一步的池项</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>池块标头大小已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0X21</p></td>
<td align="left"><p>正在释放池指针</p></td>
<td align="left"><p>对于池块分配的字节数</p></td>
<td align="left"><p>找到池块之后的损坏的值</p></td>
<td align="left"><p>正在释放池块之后的数据已损坏。 通常这意味着使用者 （调用堆栈） 具有溢出块。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0X22</p></td>
<td align="left"><p>正在释放地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>要释放的地址不具有跟踪条目。 这通常是因为调用堆栈尝试释放已释放或从未开始时分配的指针。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

在当前请求时已损坏的池。

这可能会或可能不是由于调用方。

<a name="resolution"></a>分辨率
----------

必须使用内核调试程序来找出问题的可能原因介绍了内部池链接。

然后可以为可疑的池标记中，使用特殊的池，也可以使用驱动程序验证程序上的可疑的驱动程序的"特殊池"选项。 [ **！ 分析**](-analyze.md)扩展可以是帮助查明怀疑有问题的驱动程序，但是这经常是不与池 corrupters 的情况。

使用中所述的步骤[**蓝色屏幕数据**](blue-screen-data.md)收集停止代码参数。 停止代码参数用于确定您正在跟踪的代码行为的特定类型。

**驱动程序验证程序**

驱动程序验证程序是一种工具，运行实时检查驱动程序的行为。 如果它看到错误的驱动程序代码执行过程中，它会主动创建例外以允许驱动程序代码以进行进一步仔细检查该部分。 驱动程序验证程序管理器内置于 Windows，可在所有 Windows Pc 上。 若要启动驱动程序验证程序管理器，请键入*Verifer*在命令提示符。 可以配置你想要验证的驱动程序。 验证驱动程序的代码将添加开销在运行，因此请尝试并验证尽可能最少数量的驱动程序。 有关详细信息，请参阅[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)。

**Windows 内存诊断**

如果此 Bug 检查出现不一致，它可能与有故障的物理内存。

运行 Windows 内存诊断工具，用于测试的内存。 在控件面板的搜索框中，键入内存，然后单击**诊断您的计算机的内存问题**。在测试运行后，使用事件查看器查看系统日志下的结果。 寻找*MemoryDiagnostics 结果*条目以查看结果。

 

 




