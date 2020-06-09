---
title: Bug 检查 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
description: DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN bug 检查，它指示驱动程序返回的 STATUS_REPARSE 到 IRP_MJ_CREATE 请求，但没有尾随名称。
ms.assetid: 60eeb24a-accf-4db8-ba5b-1738a9aa4b46
keywords:
- Bug 检查 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 295f9f42e0b6cc99fb9acb58713bfafa9d12b5cb
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534786"
---
# <a name="bug-check-0xf9-driver_returned_status_reparse_for_volume_open"></a>Bug 检查0xF9：驱动 \_ 程序 \_ 返回 \_ \_ 的 \_ 卷 \_ 打开状态重新分析


驱动程序 \_ 返回了 " \_ \_ \_ \_ 卷 \_ 打开 bug 检查的状态重新分析" 的值为 "0x000000F9"。 这表明驱动程序将状态重新 \_ 分析返回给 IRP \_ MJ \_ CREATE 请求，但没有尾随名称。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="driver_returned_status_reparse_for_volume_open-parameters"></a>驱动 \_ 程序 \_ 返回 \_ \_ \_ 卷 \_ 开放参数的状态重新分析


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
<td align="left"><p>已打开的设备对象</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>向其发出 IRP_MJ_CREATE 请求的设备对象</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>包含文件的新名称的 Unicode 字符串的地址（要被重新分析）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>驱动程序为 IRP_MJ_CREATE 请求返回的信息</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
\_仅应为 IRP \_ MJ \_ CREATE requests 返回带有尾随名称的状态重新分析，因为该驱动程序支持名称空间。

 

 




