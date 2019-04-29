---
title: OID_WWAN_SERVICE_ACTIVATION
description: OID_WWAN_SERVICE_ACTIVATION 指示微型端口驱动程序启动服务激活，以获取对提供程序的网络访问权限。
ms.assetid: a70c087d-0650-4aab-b78e-0d5a7aa49eb6
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SERVICE_ACTIVATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 15574dd8a63a321b7c0e07e3dfbeba068eab3a1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368453"
---
# <a name="oidwwanserviceactivation"></a>OID\_WWAN\_SERVICE\_ACTIVATION


OID\_WWAN\_服务\_激活指示微型端口驱动程序启动服务激活，以获取对提供程序的网络访问权限。

不支持查询请求。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_服务\_激活**](ndis-status-wwan-service-activation.md)状态通知包含[ **NDIS\_WWAN\_服务\_激活**](https://msdn.microsoft.com/library/windows/hardware/ff567918)结构启动服务激活，以访问提供程序的网络时他们已完成事务。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[MB 服务检测和激活](https://msdn.microsoft.com/library/windows/hardware/ff559122)。

微型端口驱动程序可以访问用户识别模块 （SIM 卡） 或提供程序网络时处理查询或设置请求。

MB 服务使用 OID\_WWAN\_服务\_在其中的服务激活过程中需要微型端口驱动程序和用户交互的情况下激活。

这不是需要启动的微型端口驱动程序或如调入服务提供商的支持人员的带外手动服务激活。 如果如上述方案中所示中激活该设备后当前微型端口驱动程序**ReadyState**是*WwanReadyStateNotActivated*，微型端口驱动程序应继续执行，与 MB 初始化和通知使用 NDIS 的就绪状态更改 MB 服务\_状态\_WWAN\_准备\_信息指示。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持微型端口驱动程序基于服务激活支持。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_READY\_INFO](oid-wwan-ready-info.md)

[**NDIS\_WWAN\_SERVICE\_ACTIVATION**](https://msdn.microsoft.com/library/windows/hardware/ff567918)

[**NDIS\_状态\_WWAN\_服务\_激活**](ndis-status-wwan-service-activation.md)

[MB 服务检测和激活](https://msdn.microsoft.com/library/windows/hardware/ff559122)

 

 




