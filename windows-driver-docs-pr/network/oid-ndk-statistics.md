---
title: OID_NDK_STATISTICS
description: 为查询，NDIS 和基础驱动程序或用户模式应用程序使用 OID_NDK_STATISTICS OID 获取 NDK 统计信息的微型端口适配器。
ms.assetid: 30F16DEC-AEE6-49D4-8599-95374ACBD446
ms.date: 08/08/2017
keywords: -OID_NDK_STATISTICS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d4a077454e36a151fa862af3391538908b106d12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576711"
---
# <a name="oidndkstatistics"></a>OID\_NDK\_统计信息


为查询，NDIS 和基础驱动程序或用户模式应用程序使用 OID\_NDK\_要获取的微型端口适配器 NDK 统计信息的统计信息 OID。

NDIS 6.30 和更高版本的微型端口驱动程序提供 NDK 服务必须支持此 OID。 否则，此 OID 是可选的。

**请注意**  NDIS 支持此 OID 与 direct 的 OID 请求接口。 有关直接 OID 请求接口的详细信息，请参阅[NDIS 6.1 直接 OID 请求接口](https://msdn.microsoft.com/library/windows/hardware/ff564736)。

 

<a name="remarks"></a>备注
-------

NDIS 发出具有此 OID **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构指向[**NDIS\_NDK\_统计信息\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451567)结构。

支持 NDK 微型端口驱动程序必须提供**CounterSet**成员，即[ **NDIS\_NDK\_性能\_计数器**](https://msdn.microsoft.com/library/windows/hardware/hh451565)结构。

计数器将发布到工具如[perfmon](https://technet.microsoft.com/library/cc731067.aspx) (请参阅[NetworkDirect 活动](https://technet.microsoft.com/library/hh997022.aspx)性能计数器)，并可通过编程方式使用的性能数据助手 (PDH) 和性能库 (PERFLIB) 编程接口。 有关这些接口的详细信息，请参阅[性能计数器](https://msdn.microsoft.com/library/windows/desktop/aa373083)。

这些计数器也有通过调用[Get NetAdapterStatistics](https://technet.microsoft.com/library/jj130889) PowerShell cmdlet **RdmaStatistics**属性。 有关详细信息**RdmaStatistics**属性，请参阅[ **MSFT\_NetAdapterStatisticsSettingData**](https://msdn.microsoft.com/library/hh872390)。

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
<td><p>无受支持的版本</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>版本</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[内核模式性能监视](https://msdn.microsoft.com/library/windows/hardware/ff548159)

[**NDIS\_NDK\_性能\_计数器**](https://msdn.microsoft.com/library/windows/hardware/hh451565)

[**NDIS\_NDK\_STATISTICS\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh451567)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

 

 




