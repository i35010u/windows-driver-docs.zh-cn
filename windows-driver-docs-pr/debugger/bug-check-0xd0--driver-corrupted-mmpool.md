---
title: Bug 检查 0xD0 DRIVER_CORRUPTED_MMPOOL
description: DRIVER_CORRUPTED_MMPOOL bug 检查具有 0x000000D0 值。 这表示系统尝试访问无效内存过高的 IRQL 的进程时。
ms.assetid: fad53a11-d4db-4f2c-b03e-19c5db47975b
keywords:
- Bug 检查 0xD0 DRIVER_CORRUPTED_MMPOOL
- DRIVER_CORRUPTED_MMPOOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CORRUPTED_MMPOOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0d87d85eebaf414ce7e6a4aa25afde823baf81c
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518888"
---
# <a name="bug-check-0xd0-drivercorruptedmmpool"></a>Bug 检查 0xD0：驱动程序\_损坏\_MMPOOL


该驱动程序\_损坏\_MMPOOL bug 检查的值为 0x000000D0。 这表示系统尝试访问无效内存过高的 IRQL 的进程时。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="drivercorruptedmmpool-parameters"></a>驱动程序\_损坏\_MMPOOL 参数


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
<td align="left"><p>引用的内存</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>在引用的时间的 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>引用内存的地址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

尝试访问可分页内存 （或可能是完全无效的内存） 内核 IRQL 时过高。 此问题的最终原因几乎可以肯定是损坏了系统池的驱动程序。

在大多数情况下，此 bug 检查结果如果驱动程序损坏了分配大量的 (页\_大小或更大)。 较小的分配会导致[ **bug 检查 0xC5** ](bug-check-0xc5--driver-corrupted-expool.md) (驱动程序\_损坏\_EXPOOL)。

<a name="resolution"></a>分辨率
----------

如果您最近安装了任何新的软件，检查以查看是否已正确安装。 检查更新的驱动程序制造商的网站上。

若要调试此错误，使用驱动程序验证程序的特殊池选项。 如果该操作未显示导致该错误的驱动程序，使用全局标志实用工具启用特殊的池的池标记。

有关特殊的池的信息，请查阅 Windows 驱动程序工具包的驱动程序验证程序部分。

另一种方法是打开 **\\ \\HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\会话管理器\\内存管理**注册表项。 在此密钥，创建或编辑**ProtectNonPagedPool**值，并将其设置为 dword 值 1。 然后重新启动。 然后系统将取消映射所有已释放的非分页缓冲的池。 这将防止驱动程序损坏该池。 （这不能防止池 DMA 硬件，但是。）

 

 




