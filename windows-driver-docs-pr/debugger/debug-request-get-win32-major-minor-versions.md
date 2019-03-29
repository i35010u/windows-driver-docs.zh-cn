---
title: 调试\_请求\_获取\_WIN32\_主要\_次要\_版本
description: 调试\_请求\_获取\_WIN32\_主要\_次要\_版本
ms.assetid: 3764add2-a96a-41c8-9747-6a1ef3d8b5af
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
ms.openlocfilehash: f9a905dac30e8584243a4b60e72887aded34503f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576000"
---
# <a name="debugrequestgetwin32majorminorversions"></a>调试\_请求\_获取\_WIN32\_主要\_次要\_版本


调试\_请求\_获取\_WIN32\_主要\_次要\_版本[**请求**](request.md)操作返回在目标系统当前正在运行的 Windows 版本。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
不使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
主版本号和次版本号在目标系统当前正在运行的 Windows 版本。 版本编号的类型是数组，其中包含两个 ULONG 值;数组中的第一个 ULONG 是主版本号和第二个是次要版本号

下表按操作系统列出的主版本号和次版本号。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">主版本号</th>
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

 

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**请求**](request.md)

 

 






