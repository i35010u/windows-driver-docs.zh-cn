---
title: 设置特定于设备的参数
description: 设置特定于设备的参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f16f65d40e5d34cee72855c05984a6d359796d72
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795895"
---
# <a name="setting-device-specific-parameters"></a>设置特定于设备的参数





在不需要在主机上配置参数的情况下，大多数远程 NDIS 设备都能正常工作。 但是，在某些情况下，正确的网络操作需要主机上的某些配置。 如果设备支持可配置参数，则它应在其所报告的支持 oid 列表中包含以下可选 OID，以响应对 OID 生成 [ \_ 支持的 \_ \_ 列表](./oid-gen-supported-list.md)的查询：

```C++
#define OID_GEN_RNDIS_CONFIG_PARAMETER 0x0001021B
```

如果设备支持 [oid \_ GEN \_ RNDIS \_ CONFIG \_ 参数](./oid-gen-rndis-config-parameter.md) OID，则主机将使用它来设置特定于设备的参数，在设备进入从未初始化状态远程 NDIS 初始化的状态之后不久。 主机将向设备发送零个或更多远程 \_ NDIS \_ 设置 \_ 消息，并将 oid \_ GEN \_ RNDIS \_ CONFIG \_ 参数作为要设置的 oid 值。 每个这样的 [**远程 \_ NDIS \_ SET \_ MSG**](/previous-versions/ff570654(v=vs.85)) 都对应于在主机上配置的一个特定于设备的参数。

与每个此类 [**远程 \_ NDIS \_ SET \_ MSG**](/previous-versions/ff570654(v=vs.85))关联的 *InformationBuffer* 采用以下格式。 请注意，偏移值相对于信息缓冲区的开头。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">大小</th>
<th align="left">字段</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterNameOffset</p></td>
<td align="left"><p>指定 ParameterNameOffset 字段开头的字节偏移量，其中表示参数名称的 Unicode 字符串位于该字段。 字符串不包括 NULL 终止符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterNameLength</p></td>
<td align="left"><p>指定参数名称字符串的字节长度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterType</p></td>
<td align="left"><p>指定参数值的数据类型。 这是以下值之一： 0-数值;2-字符串值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>12</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterValueOffset</p></td>
<td align="left"><p>指定参数值所在的 ParameterNameOffset 字段开头的字节偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterValueLength</p></td>
<td align="left"><p>指定参数值的字节长度。</p></td>
</tr>
</tbody>
</table>

 

在应用参数值之后，设备将为响应每个 [**远程 \_ ndis \_ Set \_ MSG**](/previous-versions/ff570654(v=vs.85))发送 [**远程 \_ ndis \_ 集 \_ CMPLT**](/previous-versions/ff570651(v=vs.85)) 。 如果参数设置为可接受，则它将 \_ \_ 在响应中返回状态 "成功"。 如果参数设置不是可接受的，并且设备无法应用此参数的有用默认值，则设备将返回相应的错误状态值 (请参阅状态值) 部分。 如果返回错误状态，则主机将启动设备的暂停进程。

应在 Windows 注册表中配置特定于设备的参数。 在设备安装过程中，通常会在注册表中创建用于定义参数值的键。 在设备的 INF 文件中指定密钥的列表、类型信息、默认值以及可选的有效值范围。 有关使用 INF 在网络设备的注册表中设置配置参数的详细信息，请参阅 Windows 2000 驱动程序开发工具包 (DDK) 。

 

