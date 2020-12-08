---
title: 调试 \_ 请求 \_ 获取 \_ WIN32 \_ 主要 \_ 次要 \_ 版本
description: 调试 \_ 请求 \_ 获取 \_ WIN32 \_ 主要 \_ 次要 \_ 版本
keywords:
- DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f466c0897efe83d1f23b38146eb2ceed0a923cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791635"
---
# <a name="debug_request_get_win32_major_minor_versions"></a>调试 \_ 请求 \_ 获取 \_ WIN32 \_ 主要 \_ 次要 \_ 版本


"调试 \_ 请求 \_ 获取 \_ WIN32 \_ 主要 \_ 次要 \_ 版本" [**请求**](request.md) 操作返回目标上当前正在运行的 Windows 的版本。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
未使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
当前在目标上运行的 Windows 版本的主版本号和次版本号。 版本号的类型是一个包含两个 ULONG 值的数组;数组中的第一个 ULONG 是主版本号，第二个是次要版本号

下表列出了操作系统的主版本号和次版本号。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 的版本</th>
<th align="left">主要版本号</th>
<th align="left">次版本号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2003</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>2</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**Request**](request.md)

 

 






