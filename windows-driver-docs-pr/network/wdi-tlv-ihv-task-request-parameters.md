---
title: WDI_TLV_IHV_TASK_REQUEST_PARAMETERS
description: WDI_TLV_IHV_TASK_REQUEST_PARAMETERS 是 TLV NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 包含请求的优先级。
ms.assetid: C33CF8FE-EDBC-41D1-A63C-E43650E9570E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IHV_TASK_REQUEST_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 60a227b1c4a58f931d6e19e80e745abfbc956eb8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380789"
---
# <a name="wditlvihvtaskrequestparameters"></a>WDI\_TLV\_IHV\_TASK\_REQUEST\_PARAMETERS


WDI\_TLV\_IHV\_任务\_请求\_参数是包含的请求的优先级 TLV [NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-ihv-task-request)。

## <a name="tlv-type"></a>TLV 类型


0xDF

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 此任务 IHV 请求的优先级。 请参阅[ **WDI\_IHV\_任务\_优先级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_ihv_task_priority)有效的优先级值。 |

 

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

 

 




