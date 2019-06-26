---
title: OID_WWAN_DRIVER_CAPS
description: OID_WWAN_DRIVER_CAPS 返回微型端口驱动程序支持的 MB 驱动程序模型的版本。
ms.assetid: 2310a341-6899-44ad-8dfb-a13fd0c42dcb
ms.date: 08/08/2017
keywords: -OID_WWAN_DRIVER_CAPS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 14b378f5d8b4518b315bc865c826fe9bcc650d2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385496"
---
# <a name="oidwwandrivercaps"></a>OID\_WWAN\_DRIVER\_CAPS


OID\_WWAN\_驱动程序\_CAPS 返回微型端口驱动程序支持的 MB 驱动程序模型的版本。

不支持组的请求。

微型端口驱动程序处理 OID\_WWAN\_驱动程序\_指针顶端才以同步方式，应立即返回其中的响应缓冲区包含[ **NDIS\_WWAN\_驱动程序\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps)结构，描述完成查询请求时由微型端口驱动程序实现的 MB 驱动程序模型的版本。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[MB 微型端口驱动程序初始化](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)。

微型端口驱动程序不能访问提供程序网络或用户识别模块 （SIM 卡），处理查询操作时。

MB 驱动程序模型版本的当前版本定义通过 WWAN\_主要\_版本和 WWAN\_次要\_版本\#定义令牌。 如果微型端口驱动程序返回 MB 服务不支持的 MB 驱动程序模型的版本，MB 服务将忽略该设备。

当 MB 服务是初始化或重新启动时，微型端口驱动程序可能已加载。 在这种情况下，MB 服务查询 MB 驱动程序模型实现的版本的微型端口驱动程序然后再继续颁发任何其他 Oid。 在任何会话的开始处发生这种情况。

微型端口驱动程序应返回 NDIS\_状态\_不\_在任何初始化错误的情况下受支持。 如果微型端口驱动程序返回 NDIS\_状态\_不\_支持，MB 服务将忽略设备和任何其他 Oid 将不会继续。

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


[MB 微型端口驱动程序初始化](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)

[**NDIS\_WWAN\_DRIVER\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps)

 

 




