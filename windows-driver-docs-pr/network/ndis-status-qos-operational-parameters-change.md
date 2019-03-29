---
title: NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE
description: 支持 NDIS 服务质量 (QoS) 的微型端口驱动程序发出 NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE 状态指示其操作的 NDIS QoS 参数是解决第一次或更高版本更改时。
ms.assetid: 15D2B139-1AEA-4252-8599-0EA4ED2E3733
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c4dec947ec172e250874f3305e70b19fcdfad8a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562423"
---
# <a name="ndisstatusqosoperationalparameterschange"></a>NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改


支持 NDIS 服务质量 (QoS) 问题的微型端口驱动程序**NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**状态指示当其操作的 NDIS QoS 参数是第一次解决或以后更改。 微型端口驱动程序使用这些操作的参数，以执行 QoS 数据包传输配置网络适配器。

当微型端口驱动程序将此状态指示时，它会设置**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)为指向的结构[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构。 该驱动程序初始化其操作的 NDIS QoS 参数与此结构。

**请注意**  此 NDIS 状态指示是仅对支持 IEEE 802.1 数据中心桥接 (DCB) 接口的微型端口驱动程序有效。

 

<a name="remarks"></a>备注
-------

微型端口驱动程序问题**NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**状态指示在以下情况下：

-   微型端口驱动程序必须发出**NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**状态指示后它最初已解析其操作的 NDIS QoS 参数并使用它们配置网络适配器。

-   在此初始状态指示后, 微型端口驱动程序必须发出**NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**状态指示时其操作的 NDIS QoS 参数已发生更改。 这可以是本地或远程 NDIS QoS 参数发生更改时。

-   微型端口驱动程序从 Windows 操作系统获取本地的 NDIS QoS 参数，当数据中心桥接 (DCB) 组件 (Msdcb.sys) 发出的对象标识符 (OID) 方法请求[OID\_QOS\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451835)。 此 OID 请求包含[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构，它指定本地的 NDIS QoS 参数。

    可能的情况下，当微型端口驱动程序必须在解析其操作的 NDIS QoS 参数时将覆盖本地的 NDIS QoS 参数。 这是本地的 QoS 参数破坏正在使用的任何基础协议或技术的网络适配器上当前已启用的操作 QoS 参数尤其如此。 例如，如果通过 Ethernet (FCoE) 协议情况下，启用通过光纤通道的远程启动的网络适配器驱动程序可以重写本地 QoS 参数。

    微型端口驱动程序通知 NDIS 和基础驱动程序的意向替代本地的 NDIS QoS 参数通过发出**NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**状态指示。

    有关详细信息，请参阅[管理的 NDIS QoS 参数](https://msdn.microsoft.com/library/windows/hardware/hh464015)。

**请注意**  过量驱动程序可以使用**NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**会向状态指示确定操作的 NDIS QoS 参数。 或者，这些驱动程序还可以颁发的 OID 查询请求[OID\_QOS\_OPERATIONAL\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451832)以在任何时候获取操作的 NDIS QoS 参数。

 

有关如何微型端口驱动程序问题的信息**NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**状态指示，请参阅[指示对操作的 NDIS QoS 参数更改](https://msdn.microsoft.com/library/windows/hardware/hh451447)。

有关各种类型的 NDIS QoS 参数的详细信息，请参阅[NDIS QoS 参数的概述](https://msdn.microsoft.com/library/windows/hardware/hh440130)。

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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_QOS\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451640)

[OID\_QOS\_OPERATIONAL\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451832)

 

 




