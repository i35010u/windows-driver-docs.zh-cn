---
title: Bug 检查 0xAD VIDEO_DRIVER_DEBUG_REPORT_REQUEST
description: VIDEO_DRIVER_DEBUG_REPORT_REQUEST bug 检查的值为0x000000AD。 此 bug 检查表明在运行时视频端口代表视频驱动程序创建了非致命的小型转储。
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
ms.openlocfilehash: ed2e83a614ab44f85d3810f0cb42480ca759234c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832855"
---
# <a name="bug-check-0xad-video_driver_debug_report_request"></a>Bug 检查0xAD：视频 \_ 驱动程序 \_ 调试 \_ 报表 \_ 请求


视频 \_ 驱动程序的 " \_ 调试 \_ 报表 \_ 请求 bug 检查" 的值为 "0x000000AD"。 此 bug 检查表明在运行时视频端口代表视频驱动程序创建了非致命的小型转储。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="video_driver_debug_report_request-parameters"></a>视频 \_ 驱动程序 \_ 调试 \_ 报表 \_ 请求参数


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
<td align="left"><p>自启动时间以来请求的所有报告的数目</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

由于视频驱动程序请求了调试报表，视频端口代表视频驱动程序在运行时创建了非致命的小型转储。

视频 \_ 驱动程序 \_ 调试 \_ 报表 \_ 请求 bug 检查只能由小型转储创建引起，而不是创建完整的转储或内核转储。

 

 




