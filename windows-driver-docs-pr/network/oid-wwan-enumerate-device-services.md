---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICES
description: OID_WWAN_ENUMERATE_DEVICE_SERVICES 返回微型端口驱动程序支持的设备服务的列表。包含提供的受支持的设备列表服务 Guid 的 NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 结构 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 状态通知。
ms.assetid: 12AB2235-DDF8-44CB-BD3D-61D0FFCB4080
ms.date: 08/08/2017
keywords: -OID_WWAN_ENUMERATE_DEVICE_SERVICES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8ebec1b11f3bc654868108acd9e30f0872ccb2f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541802"
---
# <a name="oidwwanenumeratedeviceservices"></a>OID\_WWAN\_ENUMERATE\_DEVICE\_SERVICES


OID\_WWAN\_ENUMERATE\_设备\_服务返回的微型端口驱动程序支持的设备服务的列表。

不支持组的请求。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_设备\_服务\_支持\_命令**](https://msdn.microsoft.com/library/windows/hardware/hh846210)状态通知包含[ **NDIS\_WWAN\_支持\_设备\_SERVICES** ](https://msdn.microsoft.com/library/windows/hardware/hh831867)结构，它提供服务 Guid 的受支持的设备的列表。

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


[**NDIS\_状态\_WWAN\_设备\_服务\_支持\_命令**](https://msdn.microsoft.com/library/windows/hardware/hh846210)

[**NDIS\_WWAN\_SUPPORTED\_DEVICE\_SERVICES**](https://msdn.microsoft.com/library/windows/hardware/hh831867)

 

 




