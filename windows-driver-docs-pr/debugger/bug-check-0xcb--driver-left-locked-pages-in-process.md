---
title: Bug 检查 0xCB DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS
description: DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS bug 检查具有 0x000000CB 值。 这表示，驱动程序或 I/O 管理器无法释放锁定的页执行 I/O 操作后。
ms.assetid: e97d114e-c6f1-44f1-a2ad-bfa8d03dc3c7
keywords:
- Bug 检查 0xCB DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS
- DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ceced424b5d4aab307703d6c54784423a6e6737
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903547"
---
# <a name="bug-check-0xcb-driverleftlockedpagesinprocess"></a>Bug 检查 0xCB：驱动程序\_左侧\_已锁定\_页面\_IN\_过程


该驱动程序\_左侧\_已锁定\_页面\_IN\_进程错误检查的值为 0x000000CB。 这表示，驱动程序或 I/O 管理器无法释放锁定的页执行 I/O 操作后。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="driverleftlockedpagesinprocess-parameters"></a>驱动程序\_左侧\_已锁定\_页面\_IN\_过程参数


消息中列出的四个参数可以具有两个可能的含义。

如果驱动程序锁定这些页面，参数具有以下含义。

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
<td align="left"><p>驱动程序中调用地址锁定页面</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>调用方中锁定页面的驱动程序的调用地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>包含锁定的页 MDL 的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>锁定的页的数目</p></td>
</tr>
</tbody>
</table>

 

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。

如果 I/O 管理器锁定这些页面，参数具有以下含义。

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
<td align="left"><p>向其发送 IRP 堆栈顶部的驱动程序的调度例程的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>向其发送 IRP 堆栈上的顶部驱动程序的设备对象的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>包含锁定的页 MDL 的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>锁定的页的数目</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

仅当颁发此 bug 检查注册表值 **\\ \\HKEY\_本地\_机\\系统\\CurrentControlSet\\控件\\会话管理器\\内存管理\\TrackLockedPages**为 dword 值 1。 如果未设置此值，则系统将发出信息不太[ **bug 检查 0x76** ](bug-check-0x76--process-has-locked-pages.md) (进程\_HAS\_已锁定\_页面)。

从 Windows Vista 开始，此 bug 检查还可以颁发由驱动程序验证程序时启用该池跟踪选项。

 

 




