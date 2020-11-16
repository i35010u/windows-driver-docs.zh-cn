---
title: Bug 检查 0xC2 BAD_POOL_CALLER
description: BAD_POOL_CALLER bug 检查的值为0x000000C2。 这表示当前线程发出错误的池请求。
ms.assetid: 64803335-ab93-4c4d-9b30-2ec15a13303f
keywords:
- Bug 检查 0xC2 BAD_POOL_CALLER
- BAD_POOL_CALLER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BAD_POOL_CALLER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de1c3be63dc92dc0040815b8aac4c0a3fe99ebf0
ms.sourcegitcommit: 9e13d3fbc74bb75335c4d2927c55b0085e46b0ea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2020
ms.locfileid: "94639035"
---
# <a name="bug-check-0xc2-bad_pool_caller"></a>Bug 检查0xC2：错误的 \_ 池 \_ 调用方

错误 \_ 的池 \_ 调用方 bug 检查的值为0x000000C2。 这表示当前线程发出错误的池请求。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="bad_pool_caller-parameters"></a>错误的 \_ 池 \_ 调用方参数

**参数 1** 指示违规类型。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>池标记</p></td>
<td align="left"><p>当前线程请求了零字节的池分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p>
<p>0x02</p>
<p>0x04</p></td>
<td align="left"><p>指向池标头的指针</p></td>
<td align="left"><p>池标头内容的第一部分</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>池标头已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>指向池标头的指针</p></td>
<td align="left"><p>池标头内容</p></td>
<td align="left"><p>当前线程尝试释放已释放的池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>池标头内容</p></td>
<td align="left"><p>正在释放的池块的地址</p></td>
<td align="left"><p>当前线程尝试释放已释放的池。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>分配大小（以字节为单位）</p></td>
<td align="left"><p>当前线程尝试以无效的 IRQL 分配池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>池地址</p></td>
<td align="left"><p>当前线程尝试使用无效的 IRQL 释放池。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>池地址</p></td>
<td align="left"><p>分配器的标记</p></td>
<td align="left"><p>尝试免费使用的标记</p></td>
<td align="left"><p>当前线程尝试使用错误的标记来释放池内存。</p>
<p> (内存可能属于另一个组件。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0X0B</p>
<p>0x0C,</p>
<p>或0x0D</p></td>
<td align="left"><p>池地址</p></td>
<td align="left"><p>池分配的标记</p></td>
<td align="left"><p>错误的配额进程指针</p></td>
<td align="left"><p>当前线程尝试在已损坏的池分配上释放配额。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>系统地址空间的开头</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程尝试在用户模式地址释放内核池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>物理页面框架</p></td>
<td align="left"><p>最高物理页面框架</p></td>
<td align="left"><p>当前线程尝试释放未分配的非分页池地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x42</p>
<p>或0x43</p></td>
<td align="left"><p>要释放的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程尝试释放永远不在任何池中的虚拟地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x44</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程尝试释放未分配的非分页池地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x46</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程尝试释放无效的池地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x47</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>物理页面框架</p></td>
<td align="left"><p>最高物理页面框架</p></td>
<td align="left"><p>当前线程尝试释放未分配的非分页池地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x48</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>当前线程尝试释放未分配的分页池地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x50</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>从页面缓冲池开头开始偏移（以页为起点）</p></td>
<td align="left"><p>页面缓冲池的大小（以字节为单位）</p></td>
<td align="left"><p>当前线程尝试释放未分配的分页池地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x60</p></td>
<td align="left"><p>开始地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程尝试释放无效的连续内存地址。</p>
<p> (<strong>MmFreeContiguousMemory</strong> 的调用方正在传递错误的指针。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x99</p></td>
<td align="left"><p>正在释放的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>当前线程尝试使用无效地址的池。</p>
<p> (此代码还可能指示池标头中的损坏。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9A</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>请求的字节数</p></td>
<td align="left"><p>池标记</p></td>
<td align="left"><p>当前线程已将分配请求标记 MUST_SUCCEED。</p>
<p> (不再支持此池类型。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9B</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>请求的字节数</p></td>
<td align="left"><p>调用方地址</p></td>
<td align="left"><p>当前线程尝试分配标记为0的池</p>
<p> (这将是时差的，可能损坏现有的标记表。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9C</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>请求的字节数</p></td>
<td align="left"><p>调用方地址</p></td>
<td align="left"><p>当前线程尝试分配标记为 "BIG" 的池。</p>
<p> (这将是时差的，可能会损坏现有的标记表。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9D</p></td>
<td align="left"><p>使用了错误的池标记</p></td>
<td align="left"><p>池类型</p></td>
<td align="left"><p>调用方地址</p></td>
<td align="left"><p>当前线程尝试使用不包含任何字母或数字的标记来分配池。 使用此类标记会导致难以跟踪池问题。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41286</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>页面中页面缓冲池起始处的起始偏移量</p></td>
<td align="left"><p>当前线程尝试在分配过程中释放分页池地址。</p></td>
</tr>
</tbody>
</table>

\_池 \_ 类型代码在 Ntddk 中进行枚举。 具体而言，0表示非分页池，1表示页面缓冲池。

## <a name="cause"></a>原因

当前线程发出了无效的池请求。 通常，这是一个错误的 IRQL 级别，或者两次释放相同的内存分配等。

## <a name="resolution"></a>解决方法

激活启用了内存池选项的驱动程序验证程序，以获取有关这些错误的详细信息并找到错误驱动程序。

**驱动程序验证程序**

驱动程序验证程序是一个实时运行的工具，用于检查驱动程序的行为。 如果发现驱动程序代码执行过程中出现错误，它会主动创建一个例外，以允许进一步审查驱动程序代码的一部分。 驱动程序验证程序管理器内置于 Windows 中，可在所有 Windows PC 上使用。 若要启动驱动程序验证程序管理器，请在命令提示下键入“验证程序”  。 你可以配置要验证的驱动程序。 验证驱动程序的代码在运行时会增加开销，因此请尝试验证尽可能少的驱动程序。 有关详细信息，请参阅[驱动程序验证程序](../devtest/driver-verifier.md)。

**Windows 内存诊断**

具体而言，对于内存池损坏的情况，请运行 Windows 内存诊断工具，尝试将物理内存作为一个原因进行隔离。 在 "控制面板" 搜索框中键入 "内存"，然后选择 " **诊断计算机的内存问题** "。运行测试后，使用事件查看器查看系统日志下的结果。 查找“内存诊断结果”条目以查看结果  。
