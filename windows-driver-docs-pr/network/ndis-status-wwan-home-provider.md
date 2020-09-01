---
title: NDIS_STATUS_WWAN_HOME_PROVIDER
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_HOME_PROVIDER 通知来通知 MB 服务 OID_WWAN_HOME_PROVIDER \ 160;查询请求。
ms.assetid: a5733c62-be4e-4f86-9639-6addd31baf0c
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_HOME_PROVIDER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8f3aa647609874765fe02d8df796c1511fcaa17a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212847"
---
# <a name="ndis_status_wwan_home_provider"></a>NDIS \_ 状态 \_ WWAN \_ 主 \_ 提供程序


微型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ home \_ 提供程序通知来通知 MB 服务完成[OID \_ WWAN \_ 主 \_ 提供程序](oid-wwan-home-provider.md)   查询请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ HOME \_ PROVIDER**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider) 结构。

<a name="remarks"></a>备注
-------

响应 OID \_ WWAN \_ 主 \_ 提供程序查询请求时，微型端口驱动程序必须符合以下规则：

-   基于 GSM 的设备：可以使用多种方法从订阅服务器标识模块 (SIM) 中检索 home 提供程序名称， (例如，在 "服务提供商名称") 下的 "3GPP TS 31.102" 中的 "TS" 中定义，或在未预配 EFSPN 时来自特定于操作员的扩展中的 "EFSPN"。 你应参考特定于操作员的要求规范来获取 home 提供程序名称、从 IMSI 提取 MCC MNC，以及在 GSMA 的数据库中执行查找。 如果未设置 EFSPN，则在检索操作员特定的主提供程序名称时，请联系运算符。 如果未通过 EFSPN 或任何其他机制将 SIM 预配到 home 提供程序名称，微型端口驱动程序应将提供程序名称设置为 **NULL**。

    有关 SIM 卡文件系统的详细信息，请参阅 3GPP TS 11.11 规范。 如果未在订阅服务器标识模块 (SIM 卡) 中设置提供程序标识，微型端口驱动程序应返回 WWAN \_ 状态 \_ 读取 \_ 失败。

-   基于 CDMA 的设备：返回 home 提供程序名称是必需的。 建议 Ihv 在其设备中将此信息作为网络个性化的一部分提供。 如果提供程序标识不可用，则基于 CDMA 的提供 **程序的微型** 端口驱动程序必须将 NDIS \_ WWAN 主提供程序结构的成员设置 \_ \_ 为 WWAN \_ CDMA \_ 默认提供程序 \_ \_ ID。

当设备就绪状态更改为 **WwanReadyStateInitialized** ，并 \_ 根据需要设置 WWAN 提供程序结构的所有成员的格式时，微型端口驱动程序必须返回此信息。

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
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WWAN \_ HOME \_ 提供程序](oid-wwan-home-provider.md)

[**NDIS \_ WWAN \_ HOME \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)

 

