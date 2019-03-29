---
title: Bug 检查 0xD2 BUGCODE_ID_DRIVER
description: BUGCODE_ID_DRIVER bug 检查具有 0x000000D2 值。 这表示与的 NDIS 驱动程序出现问题。
ms.assetid: 697d128c-c79d-454a-a3e7-e9b85e3ab4bc
keywords:
- Bug 检查 0xD2 BUGCODE_ID_DRIVER
- BUGCODE_ID_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_ID_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4d5827981537496860abf8e254f1ef8f40c24660
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350386"
---
# <a name="bug-check-0xd2-bugcodeiddriver"></a>Bug 检查 0xD2：BUGCODE\_ID\_驱动程序


BUGCODE\_ID\_驱动程序 bug 检查的值为 0x000000D2。 这表示与的 NDIS 驱动程序出现问题。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="bugcodeiddriver-parameters"></a>BUGCODE\_ID\_驱动程序参数


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
<th align="left">消息和原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>请求的字节数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>分配在引发 IRQL 共享的内存。</strong> 驱动程序调用<strong>NdisMAllocateSharedMemory</strong> IRQL 与&gt;= DISPATCH_LEVEL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p><em>状态</em>值提交到<strong>NdisMResetComplete</strong></p></td>
<td align="left"><p><em>AddressingReset</em>值提交到<strong>NdisMResetComplete</strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>正在重置完成时未挂起。</strong> 驱动程序调用<strong>NdisMResetComplete</strong>，但不重置已挂起。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>包含地址被释放的内存页</p></td>
<td align="left"><p>共享的内存签名的地址</p></td>
<td align="left"><p>要释放的虚拟地址</p></td>
<td align="left"><p><strong>释放未分配的共享的内存。</strong> 驱动程序调用<strong>NdisMFreeSharedMemory</strong>或<strong>NdisMFreeSharedMemoryAsync</strong>与的地址不位于 NDIS 共享内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>错误地包含在数据包数组中的数据包的地址</p></td>
<td align="left"><p>数据包数组的地址</p></td>
<td align="left"><p>数组中的数据包数</p></td>
<td align="left"><p><strong>指示不归它的数据包。</strong> 微型端口的数据包数组已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MiniBlock 的地址</p></td>
<td align="left"><p>驱动程序对象的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>NdisAddDevice:AddDevice</strong>使用调用<strong>MiniBlock</strong>不在<strong>NdisMiniDriverList</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MiniBlock 的地址</p></td>
<td align="left"><p>MiniBlock 的引用计数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>NdisMUnload:MiniBlock</strong>获取卸载，但它仍然位于<strong>NdisMiniDriverList</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>内存页</p></td>
<td align="left"><p>包装器上下文</p></td>
<td align="left"><p>共享的内存签名的地址</p></td>
<td align="left"><p><strong>覆盖了过去的分配的共享的内存。</strong> 正在写入到的地址不位于 NDIS 共享内存。</p></td>
</tr>
</tbody>
</table>

 

在以下情况下检查此错误，参数的含义取决于消息和参数 4 的值。

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
<th align="left">消息和原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>微型端口中断地址</p></td>
<td align="left"><p>微型端口计时器队列地址</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>在不取消中断的情况下卸载。</strong> 微型端口驱动程序将其初始化失败而无需取消注册它的中断。</p></td>
</tr>
<tr class="even">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>微型端口计时器队列地址</p></td>
<td align="left"><p>微型端口中断地址</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>在不取消中断的情况下卸载。</strong> 微型端口驱动程序未取消它的中断注册在终止过程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>微型端口中断地址</p></td>
<td align="left"><p>微型端口计时器队列地址</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>卸载而无需取消注册计时器。</strong> 微型端口驱动程序失败且不会成功取消所有计时器其初始化。</p></td>
</tr>
<tr class="even">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>微型端口计时器队列地址</p></td>
<td align="left"><p>微型端口中断地址</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>卸载而无需取消注册计时器。</strong> 微型端口驱动程序不成功取消所有计时器情况下已暂停。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在 Windows 2000 和 Windows XP 仅发生此错误检查代码。 在 Windows Server 2003 和更高版本，对应的代码是[ **bug 检查 0x7C** ](bug-check-0x7c--bugcode-ndis-driver.md) (BUGCODE\_NDIS\_驱动程序)。

在调试内部版本的 Windows，仅**引发的 IRQL 在分配共享内存**和**完成重置时一个处于未挂起状态**可能发生此错误检查的实例。 Bug 中涉及的其他实例检查 0xD2 替换 assert 语句。 请参阅[中断到调试器](breaking-into-the-debugger.md)有关详细信息。

 

 




