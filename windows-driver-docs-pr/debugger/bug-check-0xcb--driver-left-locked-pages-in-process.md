---
title: Bug 检查 0xCB DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS
description: DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS bug 检查的值为0x000000CB。 这表明驱动程序或 i/o 管理器未能在 i/o 操作后释放锁定页。
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
ms.openlocfilehash: 6634f11c57588677f51eea86acc46cc3b7b16c9f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825223"
---
# <a name="bug-check-0xcb-driver_left_locked_pages_in_process"></a>Bug 检查0xCB：驱动程序已 \_ \_ 锁定 \_ \_ 正在 \_ 处理的页


" \_ \_ \_ 进程 bug 检查" 中的驱动程序 "已锁定" 页的值为 \_ " \_ 0x000000CB"。 这表明驱动程序或 i/o 管理器未能在 i/o 操作后释放锁定页。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_left_locked_pages_in_process-parameters"></a>驱动 \_ 程序 \_ \_ \_ 在 \_ 进程参数中已锁定页


消息中列出的四个参数可以有两个可能的含义。

如果驱动程序锁定了这些页面，则这些参数具有以下含义。

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
<td align="left"><p>在锁定页面的驱动程序中调用地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>锁定页面的驱动程序中调用地址的调用方</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>包含锁定页面的 MDL 的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>锁定页面数</p></td>
</tr>
</tbody>
</table>

 

如果能够识别出导致错误的驱动程序，则其名称将打印在蓝屏上，并存储在内存中的 (PUNICODE\_STRING) KiBugCheckDriver  位置。

如果 i/o 管理器锁定了这些页面，则这些参数具有以下含义。

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
<td align="left"><p>将 IRP 发送到的堆栈上顶层驱动程序的调度例程的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>将 IRP 发送到的堆栈上顶层驱动程序的设备对象的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>包含锁定页面的 MDL 的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>锁定页面数</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

仅当注册表值 **\\ \\ HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ 会话管理器 \\ 内存管理 \\ TrackLockedPages** 等于 DWORD 1 时，才发出此 bug 检查。 如果未设置此值，则系统将发出不太丰富的 [**bug 检查 0x76**](bug-check-0x76--process-has-locked-pages.md) (进程 \_ 已 \_) 锁定 \_ 页面。

从 Windows Vista 开始，如果启用了池跟踪选项，此错误检查还可以由驱动程序验证程序发出。

 

 




