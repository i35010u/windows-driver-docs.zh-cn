---
title: OID_WWAN_HOME_PROVIDER
description: OID_WWAN_HOME_PROVIDER 用于设置和检索有关移动电话服务订阅的主提供程序的信息。
ms.assetid: f7bea146-261d-4d01-9fd5-ae512a1ac083
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_HOME_PROVIDER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0c136454ac9a65c85b519b7af9a59123574c2be1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210105"
---
# <a name="oid_wwan_home_provider"></a>OID \_ WWAN \_ HOME \_ 提供程序


OID \_ WWAN \_ HOME \_ 提供程序用于设置和检索有关移动电话服务订阅的主提供程序的信息。 对于基于 GSM 的设备和带有 U 边缘的基于 CDMA 的设备，应将此信息存储在订阅服务器标识模块 (SIM 卡) 中。 对于不带中的基于 CDMA 的设备，应将此信息存储在辅助设备内存中。

Windows 8 支持 *set* 和 *query* 请求。 Windows 7 仅支持 *查询* 请求。

微型端口驱动程序必须异步处理 *集* 请求和 *查询* 请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，并在以后发送 [**ndis \_ 状态 \_ WWAN \_ 主 \_ 提供程序**](ndis-status-wwan-home-provider.md) 状态通知、用于 *查询*或 ndis \_ 状态 \_ Wwan \_ 设置主提供程序 " \_ \_ \_ 完成状态通知" （对于 *集*），其中包含 [**ndis \_ wwan \_ 主 \_ **](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider) 提供程序结构，以将有关家庭网络提供 **程序的** 信息返回 \_ 到 " \_ \_ WWAN 提供程序 \_ 状态" \_ \_ 主页。

仅支持多运营商的设备需要*设置*操作。 MB 服务将仅将主提供程序 *设置* 为通过 OID \_ wwan \_ 首选 \_ 多 \_ 提供程序或 oid \_ wwan \_ 可见 \_ 提供程序由小型端口报告的多运营商提供商。 *Set* 操作具有 NDIS \_ WWAN \_ Set \_ HOME \_ 提供程序的输入缓冲区。

<a name="remarks"></a>备注
-------

无论当前 SIM 或目标 SIM 是否处于锁定状态， *设置* 操作都不应要求用户对设备解锁。

| 当前提供程序 SIM | 目标提供程序 SIM | *设置*主 \_ 提供程序的结果                               |
|----------------------|---------------------|--------------------------------------------------------------|
| -                    | 已锁定              | 设置 home 提供程序不需要目标 PIN            |
| 已锁定               | -                   | 设置 home 提供程序不需要源 PIN            |
| 已锁定               | 已锁定              | 设置 home 提供程序不需要源和目标 PIN |

 

有关使用此 OID 的详细信息，请参阅 [WWAN 提供程序操作](./mb-provider-operations.md)。

当处理查询操作时，微型端口驱动程序可以 (SIM 卡) 访问订阅服务器标识模块，但不应访问提供程序网络。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ WWAN \_ HOME \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)

[**NDIS \_ 状态 \_ WWAN \_ 主 \_ 提供程序**](ndis-status-wwan-home-provider.md)

[WWAN 提供程序操作](./mb-provider-operations.md)

 

