---
title: OID_WWAN_DEVICE_SERVICE_SESSION_WRITE
description: OID_WWAN_DEVICE_SERVICE_SESSION_WRITE 指示要为设备服务会话将数据写入到 MB 设备的微型端口驱动程序。包含描述该操作的完成状态的 NDIS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 结构 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 状态通知。
ms.assetid: C1389D7D-3C8E-41B5-8E00-617D699699A2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICE_SESSION_WRITE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a29090183bda9af12d9808898d9b1219375f28c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548054"
---
# <a name="oidwwandeviceservicesessionwrite"></a>OID\_WWAN\_DEVICE\_SERVICE\_SESSION\_WRITE


OID\_WWAN\_设备\_服务\_会话\_写指示要为设备服务会话将数据写入到 MB 设备的微型端口驱动程序。

不支持查询请求。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_设备\_服务\_会话\_编写\_完成**](https://msdn.microsoft.com/library/windows/hardware/hh846208)状态通知，其中包含[ **NDIS\_WWAN\_设备\_服务\_会话\_编写\_完成**](https://msdn.microsoft.com/library/windows/hardware/hh831861)描述结构操作的完成状态。

微型端口驱动程序应返回 NDIS\_状态\_适配器\_不\_打开如果设备服务会话不处于打开状态。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>版本：支持 Windows 8 和更高版本的 Windows 中。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_状态\_WWAN\_设备\_服务\_会话\_编写\_完成**](https://msdn.microsoft.com/library/windows/hardware/hh846208)

[**NDIS\_WWAN\_DEVICE\_SERVICE\_SESSION\_WRITE**](https://msdn.microsoft.com/library/windows/hardware/hh831860)

 

 




