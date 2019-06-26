---
title: OID_WWAN_HOME_PROVIDER
description: OID_WWAN_HOME_PROVIDER 用于设置和检索有关家庭的提供程序的移动电话服务订阅的信息。
ms.assetid: f7bea146-261d-4d01-9fd5-ae512a1ac083
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_HOME_PROVIDER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ce988d17929cb4082e9cf6bd7d78889e2c69fbee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360237"
---
# <a name="oidwwanhomeprovider"></a>OID\_WWAN\_主页\_提供程序


OID\_WWAN\_家庭\_提供程序用于设置和检索有关家庭的提供程序的移动电话服务订阅的信息。 为基于 GSM 的设备和 U RIM 与基于 CDMA 的设备，此信息应存储在用户识别模块 （SIM 卡）。 为基于 CDMA 的设备，无需 U RIM，应在辅助设备内存中存储此信息。

Windows 8 同时支持两者*设置*并*查询*请求。 仅支持 Windows 7*查询*请求。

微型端口驱动程序必须处理两者*设置*并*查询*请求一开始，以异步方式返回 NDIS\_状态\_指示\_所需的原始请求和更高版本发送[ **NDIS\_状态\_WWAN\_主页\_提供程序**](ndis-status-wwan-home-provider.md)状态通知，为*查询*，或 NDIS\_状态\_WWAN\_设置\_主页\_提供程序\_的完成状态通知*设置*，其中包含[ **NDIS\_WWAN\_家庭\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)结构返回有关与家庭网络提供程序的信息**Provider.ProviderState**成员的 NDIS\_WWAN\_主页\_提供程序结构设置为 WWAN\_提供程序\_状态\_主页。

*设置*操作仅需要支持通过多运营商、 支持的设备。 MB 服务将仅*设置*多运营商提供程序的主页提供程序报告通过 OID 微型端口\_WWAN\_首选\_多\_提供程序或 OID\_WWAN\_VISIBLE\_提供程序。 *设置*操作具有输入的缓冲区的 NDIS\_WWAN\_设置\_主页\_提供程序。

<a name="remarks"></a>备注
-------

一个*设置*操作应该不需要用户解锁而不考虑设备，如果当前 SIM 或目标 SIM 处于锁定状态。

| 当前提供程序 SIM | 目标提供程序 SIM | 结果*设置*主页\_提供程序                               |
|----------------------|---------------------|--------------------------------------------------------------|
| -                    | 已锁定              | 设置家庭提供程序不需要目标 PIN            |
| 已锁定               | -                   | 设置家庭提供程序不需要源 PIN            |
| 已锁定               | 已锁定              | 源和目标不设置家庭的提供程序所需的 PIN |

 

有关使用此 OID 的详细信息，请参阅[WWAN 提供程序操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)。

微型端口驱动程序可以访问用户识别模块 （SIM 卡） 当处理查询操作，但不是应访问提供程序网络。

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


[**NDIS\_WWAN\_HOME\_PROVIDER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)

[**NDIS\_状态\_WWAN\_主页\_提供程序**](ndis-status-wwan-home-provider.md)

[WWAN 提供程序操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




