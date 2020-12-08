---
title: NDIS_STATUS_WDI_INDICATION_TASK_OFFLOAD_CURRENT_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_TASK_OFFLOAD_CURRENT_CONFIG 来表明硬件的 TCP 卸载功能发生变化。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_TASK_OFFLOAD_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 97c5ac78d05f58892c0087c5f653c5ef2e00944f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786735"
---
# <a name="ndis_status_wdi_indication_task_offload_current_config"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 任务 \_ 卸载 \_ 当前 \_ 配置


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ 任务 \_ 卸载 \_ 当前 \_ 配置，以指示硬件的 TCP 卸载功能发生更改的时间。

| 对象 |
|--------|
| 端口   |

 

当硬件的 TCP 卸载功能发生变化时，LE 使用新的 TCP 校验和/LSO 功能向 UE 发送此未经请求的指示。 对于 [**WDI \_ TLV \_ TCP \_ 卸载 \_ 功能**](./wdi-tlv-tcp-offload-capabilities.md)中的成员，使用 " **ndis \_ 卸载 \_ 集已 \_ 关闭**" 和 **\_ "ndis 卸载 \_ 集 \_** " 的值，以指示卸载功能的更改。 当 UE 发送 [OID \_ WDI \_ 设置 \_ TCP \_ 卸载 \_ 参数](oid-wdi-set-tcp-offload-parameters.md)时，该 LE 应更新卸载功能，然后发送此指示，以便使用最新的卸载功能信息更新 OS。

## <a name="payload-data"></a>负载数据


| 类型                                                                                  | 允许多个 TLV 实例 | 可选 | 说明                                              |
|---------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------|
| [**WDI \_ TLV \_ TCP \_ 卸载 \_ 功能**](./wdi-tlv-tcp-offload-capabilities.md) |                                | X        | TCP/IP 校验和和大型发送卸载功能。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WDI \_ 设置 \_ TCP \_ 卸载 \_ 参数](oid-wdi-set-tcp-offload-parameters.md)

 

