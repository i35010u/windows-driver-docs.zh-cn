---
title: WDI_TLV_ASSOCIATION_REQUEST_DEVICE_CONTEXT
description: WDI_TLV_ASSOCIATION_REQUEST_DEVICE_CONTEXT 是包含特定于供应商的信息传递到端口如果主机决定发送对传入的关联请求的响应 TLV。
ms.assetid: 5C684769-77A0-446D-81F6-A90E54806A1F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_REQUEST_DEVICE_CONTEXT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7938af034d1300c284ad7ae0f3320866a9aec07e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362841"
---
# <a name="wditlvassociationrequestdevicecontext"></a>WDI\_TLV\_ASSOCIATION\_REQUEST\_DEVICE\_CONTEXT


WDI\_TLV\_关联\_请求\_设备\_上下文是包含特定于供应商的信息传递到端口如果主机决定将响应发送到传入 TLV关联的请求。

## <a name="tlv-type"></a>TLV 类型


0x72

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                                           |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 向下传递如果主机决定将传入的关联请求响应发送端口的特定于供应商的信息。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




