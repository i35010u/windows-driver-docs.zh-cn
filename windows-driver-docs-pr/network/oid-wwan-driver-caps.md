---
title: OID_WWAN_DRIVER_CAPS
description: OID_WWAN_DRIVER_CAPS 返回微型端口驱动程序支持的 MB 驱动程序型号版本。
ms.assetid: 2310a341-6899-44ad-8dfb-a13fd0c42dcb
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DRIVER_CAPS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6ea5310a837756060d4f3237d1acc24a412e1685
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843848"
---
# <a name="oid_wwan_driver_caps"></a>OID\_WWAN\_驱动程序\_CAP


OID\_WWAN\_驱动程序\_CAP 返回微型端口驱动程序所支持的 MB 驱动程序型号版本。

不支持设置请求。

微型端口驱动程序以同步方式将\_WWAN\_驱动程序的 OID 处理\_帽，并应立即返回包含[**NDIS\_WWAN\_驱动程序\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps)结构的响应缓冲区，其中描述了版本完成查询请求时，微型端口驱动程序所实现的 MB 驱动程序模型。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[MB 微型端口驱动程序初始化](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)。

处理查询操作时，微型端口驱动程序不应访问提供程序网络或订阅服务器标识模块（SIM 卡）。

MB 驱动程序型号版本的当前版本由 WWAN\_主要\_版本和 WWAN\_次要\_版本定义，\#定义令牌。 如果微型端口驱动程序返回 MB 服务不支持的 MB 驱动程序型号版本，MB 服务将忽略此设备。

如果初始化或重新启动了 MB 服务，则可能已加载微型端口驱动程序。 在这种情况下，MB 服务会查询通过微型端口驱动程序实现的 MB 驱动程序模型的版本，然后再继续发出其他任何 Oid。 此操作发生在任何会话的开头。

小型端口驱动程序应返回 NDIS\_状态\_在任何初始化错误的情况下不\_支持。 如果微型端口驱动程序返回 NDIS\_状态\_不\_支持，MB 服务将忽略该设备，并且不会继续其他任何 Oid。

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[MB 微型端口驱动程序初始化](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)

[**NDIS\_WWAN\_驱动程序\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps)

 

 




