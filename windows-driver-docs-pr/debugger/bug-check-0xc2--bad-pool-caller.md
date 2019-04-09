---
title: Bug 检查 0xC2 BAD_POOL_CALLER
description: BAD_POOL_CALLER bug 检查具有 0x000000C2 值。 它指示当前线程正在发出错误的池请求。
ms.assetid: 64803335-ab93-4c4d-9b30-2ec15a13303f
keywords:
- （开发人员内容）Bug 检查 0xC2 BAD_POOL_CALLER
- BAD_POOL_CALLER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BAD_POOL_CALLER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e4dca6534a7caa59805f9f6f0c6298d00aef3417
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239620"
---
# <a name="developer-content-bug-check-0xc2-badpoolcaller"></a>（开发人员内容）Bug 检查 0xC2:错误\_池\_调用方


缺点\_池\_bug 检查调用方的值为 0x000000C2。 它指示当前线程正在发出错误的池请求。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="badpoolcaller-parameters"></a>错误\_池\_调用方的参数


**参数 1**指示冲突类型。

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
<td align="left"><p>0x00</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>池标记</p></td>
<td align="left"><p>当前线程所请求的零字节池分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01，</p>
<p>0x02,</p>
<p>0x04</p></td>
<td align="left"><p>指向池标头</p></td>
<td align="left"><p>池标头内容的第一部分</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>池标头已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>指向池标头</p></td>
<td align="left"><p>池标头内容</p></td>
<td align="left"><p>当前线程在尝试释放已释放的池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>池标头内容</p></td>
<td align="left"><p>要释放的池的块的地址</p></td>
<td align="left"><p>当前线程在尝试释放已释放的池。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>分配，以字节为单位的大小</p></td>
<td align="left"><p>当前线程尝试在无效的 IRQL 池分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>池的地址</p></td>
<td align="left"><p>当前线程在尝试释放无效的 IRQL 在池。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>池的地址</p></td>
<td align="left"><p>分配器的标记</p></td>
<td align="left"><p>标记使用在尝试释放</p></td>
<td align="left"><p>当前线程在尝试使用错误的标记释放池内存。</p>
<p>（内存可能属于另一个组件。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0B，</p>
<p>0x0C，</p>
<p>或 0x0D</p></td>
<td align="left"><p>池的地址</p></td>
<td align="left"><p>池分配的标记</p></td>
<td align="left"><p>错误配额过程指针</p></td>
<td align="left"><p>当前线程在尝试发布已损坏的池分配的配额。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>系统地址空间的开头</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程在尝试释放在用户模式地址内核池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>物理页框架</p></td>
<td align="left"><p>最高的物理页面框架</p></td>
<td align="left"><p>当前线程在尝试释放未分配的非分页的池地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x42</p>
<p>或 0x43</p></td>
<td align="left"><p>要释放的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程在尝试释放永远不会在任何池的虚拟地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x44</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程在尝试释放未分配的非分页的池地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x46</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程在尝试释放无效池地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x47</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>物理页框架</p></td>
<td align="left"><p>最高的物理页面框架</p></td>
<td align="left"><p>当前线程在尝试释放未分配的非分页的池地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x48</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>当前线程在尝试释放未分配的非分页的池地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x50</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>开始偏移量，在页中，从页面缓冲池的开始</p></td>
<td align="left"><p>页面缓冲池，以字节为单位的大小</p></td>
<td align="left"><p>当前线程在尝试释放未分配的非分页的池地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x60</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程在尝试释放无效的连续内存地址。</p>
<p>(的调用方<strong>MmFreeContiguousMemory</strong>传递错误的指针。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x99</p></td>
<td align="left"><p>要释放的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程在尝试释放具有无效的地址池。</p>
<p>（此代码还可以指示池标头中的损坏。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9A</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>请求的字节数</p></td>
<td align="left"><p>池标记</p></td>
<td align="left"><p>当前线程标记分配请求 MUST_SUCCEED。</p>
<p>（不再支持此池类型。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9B</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>请求的字节数</p></td>
<td align="left"><p>调用方的地址</p></td>
<td align="left"><p>当前线程在尝试分配了标记的 0 的池</p>
<p>（这将是无法跟踪，并可能会损坏现有标记表。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9C</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>请求的字节数</p></td>
<td align="left"><p>调用方的地址</p></td>
<td align="left"><p>当前线程在尝试了标记"BIG"池分配。</p>
<p>（这是无法跟踪和可能可能会损坏现有标记表。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9D</p></td>
<td align="left"><p>使用不正确的池标记</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>调用方的地址</p></td>
<td align="left"><p>当前线程在尝试使用不包含任何字母或数字标记池分配。 使用此类标记使跟踪池问题很难。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41286</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>在页面的页面缓冲池从头开始偏移量</p></td>
<td align="left"><p>当前线程在尝试释放分配的中间页面缓冲的池地址。</p></td>
</tr>
</tbody>
</table>

 

\_池\_Ntddk.h 中枚举类型代码。 具体而言，0 表示非分页缓冲的池，而 1 表示页面缓冲的池。

<a name="cause"></a>原因
-----

当前线程已发出的无效池请求。 这通常是错误的 IRQL 级别或 double 释放的相同的内存分配，等等。

<a name="resolution"></a>分辨率
----------

内存池选项启用，以获取有关这些错误的详细信息，并找到出错的驱动程序使用激活驱动程序验证程序。

**驱动程序验证程序**

驱动程序验证程序是一种工具，运行实时检查驱动程序的行为。 如果它看到错误的驱动程序代码执行过程中，它会主动创建例外以允许驱动程序代码以进行进一步仔细检查该部分。 驱动程序验证程序管理器内置于 Windows，可在所有 Windows Pc 上。 若要启动驱动程序验证程序管理器，请键入*Verifer*在命令提示符。 可以配置你想要验证的驱动程序。 验证驱动程序的代码将添加开销在运行，因此请尝试并验证尽可能最少数量的驱动程序。 有关详细信息，请参阅[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)。

**Windows 内存诊断**

具体而言，与池的内存损坏的情况下，运行 Windows 内存诊断工具，用于尝试并找出原因的物理内存。 在控件面板的搜索框中，键入内存，然后单击**诊断您的计算机的内存问题**。在测试运行后，使用事件查看器查看系统日志下的结果。 寻找*MemoryDiagnostics 结果*条目以查看结果。

 

 




