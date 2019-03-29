---
title: 设置特定于设备的参数
description: 设置特定于设备的参数
ms.assetid: 5df72c11-e8d4-4e06-8f34-c9b85ad779f6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cd4cf05812dfa5ed694cc6a58c5b2c404f24a73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569028"
---
# <a name="setting-device-specific-parameters"></a>设置特定于设备的参数





应大多数远程 NDIS 设备将起作用也无需在主机上配置参数。 但是，可能有适当的网络操作，需要在主机上的某些配置的情况。 如果设备支持可配置参数，则它应在列表中的受支持的 Oid 它报告的查询响应中包括以下可选 OID [OID\_代\_支持\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569642):

```C++
#define OID_GEN_RNDIS_CONFIG_PARAMETER 0x0001021B
```

如果设备支持[OID\_代\_RNDIS\_CONFIG\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569639)OID，主机使用它来设置特定于设备的参数，则设备将进入的状态初始化之后立即通过从初始化状态的远程 NDIS。 主机将发送零个或多个远程\_NDIS\_设置\_到设备的消息数与 OID\_常规\_RNDIS\_配置\_要设置的 OID 值作为参数。 每个此类[**远程\_NDIS\_设置\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff570654)对应于在主机配置的一个特定于设备的参数。

*InformationBuffer*与每个此类相关联[**远程\_NDIS\_设置\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff570654)采用以下格式。 请注意，偏移量值相对于信息缓冲区的开头。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">偏移量</th>
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
<td align="left"><p>指定的字节偏移量从表示参数名称的 Unicode 字符字符串的 ParameterNameOffset 字段的开头。 字符串不包括 NULL 终止符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterNameLength</p></td>
<td align="left"><p>指定的参数名称字符串的字节长度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterType</p></td>
<td align="left"><p>指定参数值的数据的类型。 这是以下值之一：0-数值;2-字符串值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>12</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterValueOffset</p></td>
<td align="left"><p>指定的字节偏移量从参数值的 ParameterNameOffset 字段的开头。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterValueLength</p></td>
<td align="left"><p>指定参数值的字节长度。</p></td>
</tr>
</tbody>
</table>

 

设备发送[**远程\_NDIS\_设置\_CMPLT** ](https://msdn.microsoft.com/library/windows/hardware/ff570651)中对每个响应[**远程\_NDIS\_设置\_MSG**](https://msdn.microsoft.com/library/windows/hardware/ff570654)之后应用参数的值。 如果此参数设置为可接受的它返回的状态为 RNDIS\_状态\_成功的响应中。 如果参数的设置不是可接受的并且设备无法应用此参数，一个有用的默认值，则设备返回相应的错误状态值 （请参阅状态的值部分）。 如果返回了错误状态，则主机将启动设备的停止进程。

特定于设备的参数应在 Windows 注册表中进行配置。 定义参数值的键通常创建在注册表中的设备安装过程。 设备 INF 文件中指定的密钥、 类型信息、 默认值和可选的有效值的范围列表。 有关使用 INF 网络设备的注册表中设置配置参数的详细信息，请查阅 Windows 2000 驱动程序开发工具包 (DDK)。

 

 





