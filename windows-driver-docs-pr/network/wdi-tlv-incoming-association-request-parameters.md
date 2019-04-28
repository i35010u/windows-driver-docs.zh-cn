---
title: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS
description: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS 是 TLV，其中包含关联请求参数。
ms.assetid: DC3439A2-2221-4489-AB38-3752624EA4B2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ee261a46dc34faa5b06b3858f371991b73a671f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342277"
---
# <a name="wditlvincomingassociationrequestparameters"></a>WDI\_TLV\_传入\_关联\_请求\_参数


WDI\_TLV\_传入\_关联\_请求\_参数是包含关联请求参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x7D

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                   |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 发件人的 MAC 地址。                                                                                                |
| UINT8                                             | 指示它重新关联请求的位。 如果值为 1 指示这是一个重新关联请求。 |

 

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

 

 




