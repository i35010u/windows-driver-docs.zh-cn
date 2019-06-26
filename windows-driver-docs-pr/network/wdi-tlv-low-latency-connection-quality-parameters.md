---
title: WDI_TLV_LOW_LATENCY_CONNECTION_QUALITY_PARAMETERS
description: WDI_TLV_LOW_LATENCY_CONNECTION_QUALITY_PARAMETERS 是包含较低的延迟的连接质量参数 TLV。
ms.assetid: F6C26267-AC6F-4810-913B-46DA99498BE2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_LOW_LATENCY_CONNECTION_QUALITY_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 03faeaff0e4fa6b3c248706678da27889f7601e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354470"
---
# <a name="wditlvlowlatencyconnectionqualityparameters"></a>WDI\_TLV\_低\_延迟\_连接\_质量\_参数


WDI\_TLV\_低\_延迟\_连接\_质量\_参数是包含较低的延迟的连接质量参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0xF6

## <a name="length"></a>长度


所有包含的元素的数组大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                                                                                                                                                                                                                                                            |
|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 指定最大端口可以是另一个通道 Active 扫描或其他多渠道操作期间的毫秒数。 此关闭通道可更高版本的唯一实例是适配器需要为被动扫描。                                 |
| UINT8 | 指定的链接质量阈值[NDIS\_状态\_WDI\_指示\_漫游\_需执行](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)。 低于此阈值链接质量时，它是可接受的适配器以发送 NDIS\_状态\_WDI\_指示\_漫游\_需执行。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WDI\_设置\_连接\_质量](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-connection-quality)

[NDIS\_状态\_WDI\_指示\_漫游\_需执行](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)

 

 




