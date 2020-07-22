---
title: Bug 检查 0xD2 BUGCODE_ID_DRIVER
description: BUGCODE_ID_DRIVER bug 检查的值为0x000000D2。 这表示 NDIS 驱动程序出现问题。
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
ms.openlocfilehash: 4fae927262fcb092aab82033896302c73e2ba1e1
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873850"
---
# <a name="bug-check-0xd2-bugcode_id_driver"></a>Bug 检查0xD2： BUGCODE \_ ID \_ 驱动程序


BUGCODE \_ ID \_ 驱动程序 bug 检查的值为0x000000D2。 这表示 NDIS 驱动程序出现问题。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="bugcode_id_driver-parameters"></a>BUGCODE \_ ID \_ 驱动程序参数


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
<th align="left">消息和原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>请求的字节数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>按引发的 IRQL 分配共享内存。</strong> 一个名为<strong>NdisMAllocateSharedMemory</strong>的驱动程序，其 IRQL &gt; = DISPATCH_LEVEL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>提交给<strong>NdisMResetComplete</strong>的<em>状态值</em></p></td>
<td align="left"><p>提交给<strong>NdisMResetComplete</strong>的<em>AddressingReset</em>值</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>当某个未挂起时完成重置。</strong> 一个名为<strong>NdisMResetComplete</strong>的驱动程序，但不存在要等待的重置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>包含要释放的地址的内存页</p></td>
<td align="left"><p>共享内存签名的地址</p></td>
<td align="left"><p>正在释放虚拟地址</p></td>
<td align="left"><p><strong>释放未分配的共享内存。</strong> 一个名为<strong>NdisMFreeSharedMemory</strong>或<strong>NdisMFreeSharedMemoryAsync</strong>的驱动程序，其地址不位于 NDIS 共享内存中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>数据包数组中错误包含的数据包的地址</p></td>
<td align="left"><p>数据包数组的地址</p></td>
<td align="left"><p>数组中的数据包数</p></td>
<td align="left"><p><strong>指示未由其拥有的数据包。</strong> 微型端口的数据包数组已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MiniBlock 的地址</p></td>
<td align="left"><p>驱动程序对象的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>NdisAddDevice：</strong>使用不在<strong>NdisMiniDriverList</strong>上的<strong>MiniBlock</strong>调用 AddDevice。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MiniBlock 的地址</p></td>
<td align="left"><p>MiniBlock 的引用计数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>NdisMUnload： MiniBlock</strong>正在卸载，但它仍在<strong>NdisMiniDriverList</strong>上。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>内存页</p></td>
<td align="left"><p>包装上下文</p></td>
<td align="left"><p>共享内存签名的地址</p></td>
<td align="left"><p><strong>覆盖过的已分配共享内存。</strong> 要写入的地址不位于 NDIS shared memory 中。</p></td>
</tr>
</tbody>
</table>

 

在此 bug 检查的下列实例中，参数的含义取决于消息以及参数4的值。

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
<th align="left">消息和原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>微型端口中断的地址</p></td>
<td align="left"><p>微型端口计时器队列的地址</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>卸载但不注销中断。</strong> 小型小型驱动程序初始化失败，无需注销其中断。</p></td>
</tr>
<tr class="even">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>微型端口计时器队列的地址</p></td>
<td align="left"><p>微型端口中断的地址</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>卸载但不注销中断。</strong> 小型端口驱动程序未在暂停过程中取消注册其中断。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>微型端口中断的地址</p></td>
<td align="left"><p>微型端口计时器队列的地址</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>卸载但不取消注册计时器。</strong> 小型小型驱动程序初始化失败，未成功取消其所有计时器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>微型端口块的地址</p></td>
<td align="left"><p>微型端口计时器队列的地址</p></td>
<td align="left"><p>微型端口中断的地址</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>卸载但不取消注册计时器。</strong> 微型端口驱动程序已停止，但未成功取消其所有计时器。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

此 bug 检查代码仅出现在 Windows 2000 和 Windows XP 上。 在 Windows Server 2003 及更高版本中，对应的代码为[**bug 检查 0x7C**](bug-check-0x7c--bugcode-ndis-driver.md) （BUGCODE \_ NDIS \_ 驱动程序）。

在 Windows 的已检查内部版本中，只有在出现此 bug 检查的不挂起实例的情况下，才会在生成的 IRQL 和**完成重置时****分配共享内存**。 Bug 检查0xD2 的所有其他实例都将替换为断言。 有关详细信息，请参阅[进入调试器](breaking-into-the-debugger.md)。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。
 

 




