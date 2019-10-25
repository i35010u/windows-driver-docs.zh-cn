---
title: OID_WWAN_HOME_PROVIDER
description: OID_WWAN_HOME_PROVIDER 用于设置和检索有关移动服务订阅的主提供程序的信息。
ms.assetid: f7bea146-261d-4d01-9fd5-ae512a1ac083
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_HOME_PROVIDER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3bee8cbfcb751534bca1248166b808274c72c4c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843842"
---
# <a name="oid_wwan_home_provider"></a>OID\_WWAN\_HOME\_提供程序


OID\_WWAN\_HOME\_提供程序用于设置和检索有关移动服务订阅的主提供程序的信息。 对于基于 GSM 的设备和带有 U 边缘的基于 CDMA 的设备，此信息应存储在订阅服务器标识模块（SIM 卡）上。 对于不带中的基于 CDMA 的设备，应将此信息存储在辅助设备内存中。

Windows 8 支持*set*和*query*请求。 Windows 7 仅支持*查询*请求。

微型端口驱动程序必须异步处理*集*和*查询*请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后发送[**ndis\_状态\_WWAN\_HOME\_提供程序**](ndis-status-wwan-home-provider.md)状态通知、*查询*或 NDIS\_状态\_WWAN\_设置\_HOME\_提供程序\_完成状态通知，用于*设置*，包含[**ndis\_wwan\_home\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)结构，以返回有关使用**提供程序的 ProviderState**成员\_\_的主网络提供程序的信息。设置为 WWAN\_提供程序的提供程序结构\_状态\_HOME。

仅支持多运营商的设备需要*设置*操作。 MB 服务只会将主提供程序*设置*为通过 OID\_WWAN\_首选\_多\_提供程序或 OID\_WWAN\_可见\_提供程序报告的多个电信提供商。 *Set*操作具有 NDIS\_WWAN\_集\_HOME\_提供程序的输入缓冲区。

<a name="remarks"></a>备注
-------

无论当前 SIM 或目标 SIM 是否处于锁定状态，*设置*操作都不应要求用户对设备解锁。

| 当前提供程序 SIM | 目标提供程序 SIM | *设置*HOME\_提供程序的结果                               |
|----------------------|---------------------|--------------------------------------------------------------|
| -                    | “已锁定”，              | 设置 home 提供程序不需要目标 PIN            |
| “已锁定”，               | -                   | 设置 home 提供程序不需要源 PIN            |
| “已锁定”，               | “已锁定”，              | 设置 home 提供程序不需要源和目标 PIN |

 

有关使用此 OID 的详细信息，请参阅[WWAN 提供程序操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)。

当处理查询操作时，微型端口驱动程序可以访问订阅服务器标识模块（SIM 卡），但不应访问提供程序网络。

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


[**NDIS\_WWAN\_HOME\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)

[**WWAN\_HOME\_提供程序\_的 NDIS\_状态**](ndis-status-wwan-home-provider.md)

[WWAN 提供程序操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




