---
title: OID_WWAN_DEVICE_SERVICE_SESSION
description: OID_WWAN_DEVICE_SERVICE_SESSION 指示微型端口驱动程序打开或关闭设备服务会话。包含描述操作的结果的 NDIS_WWAN_SET_DEVICE_SERVICE_SESSION 结构 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 状态通知。
ms.assetid: 32D4EDE3-4782-4C54-95B8-83DE7E63C4F8
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICE_SESSION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 19624fffce6e9af02e24e648d8b2b60c7ed9954d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569078"
---
# <a name="oidwwandeviceservicesession"></a>OID\_WWAN\_DEVICE\_SERVICE\_SESSION


OID\_WWAN\_设备\_服务\_会话将定向微型端口驱动程序打开或关闭设备服务会话。

不支持查询请求。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_设备\_服务\_会话**](https://msdn.microsoft.com/library/windows/hardware/hh846206)状态通知包含[ **NDIS\_WWAN\_设置\_设备\_服务\_会话**](https://msdn.microsoft.com/library/windows/hardware/hh831865)结构描述操作的结果。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持指定的设备服务或操作支持。

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
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_SET\_DEVICE\_SERVICE\_SESSION**](https://msdn.microsoft.com/library/windows/hardware/hh831865)

[**NDIS\_状态\_WWAN\_设备\_服务\_会话**](https://msdn.microsoft.com/library/windows/hardware/hh846206)

 

 




