---
title: Bug 检查 0xAD VIDEO_DRIVER_DEBUG_REPORT_REQUEST
description: VIDEO_DRIVER_DEBUG_REPORT_REQUEST bug 检查具有 0x000000AD 值。 此 bug 检查指示的视频端口在运行时创建视频驱动程序代表非致命性的小型转储。
ms.assetid: eedde484-584b-478b-9429-a9c78bb62c1e
keywords:
- Bug 检查 0xAD VIDEO_DRIVER_DEBUG_REPORT_REQUEST
- VIDEO_DRIVER_DEBUG_REPORT_REQUEST
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_DRIVER_DEBUG_REPORT_REQUEST
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9a69e456f00bbb393d477506c55b286847149ba
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903949"
---
# <a name="bug-check-0xad-videodriverdebugreportrequest"></a>Bug 检查 0xAD：VIDEO\_DRIVER\_DEBUG\_REPORT\_REQUEST


视频\_驱动程序\_调试\_报表\_请求错误检查的值为 0x000000AD。 此 bug 检查指示的视频端口在运行时创建视频驱动程序代表非致命性的小型转储。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="videodriverdebugreportrequest-parameters"></a>视频\_驱动程序\_调试\_报表\_请求参数


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
<td align="left"><p>特定于驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>特定于驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>特定于驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>已请求启动以来的所有报告数</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在运行时创建视频驱动程序代表非致命性的小型转储，由于视频驱动程序请求的调试报告的视频端口。

视频\_驱动程序\_调试\_报表\_请求 bug 检查可能仅由小型转储创建，不是由创建完全转储或内核转储。

 

 




