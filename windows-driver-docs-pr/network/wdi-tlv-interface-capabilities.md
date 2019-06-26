---
title: WDI_TLV_INTERFACE_CAPABILITIES
description: WDI_TLV_INTERFACE_CAPABILITIES 是 TLV 包含 Wi-fi 接口的功能。
ms.assetid: 308331DD-FEEB-4C49-BEBD-117AE58D4792
ms.date: 02/14/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_INTERFACE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 67fb92fede631a8627d019dc8e59268566f43e9a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380756"
---
# <a name="wditlvinterfacecapabilities"></a>WDI\_TLV\_接口\_功能


WDI\_TLV\_接口\_功能是包含的功能的 Wi-fi 接口 TLV。

## <a name="tlv-type"></a>TLV 类型

0xF

## <a name="length"></a>长度

所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT32 | 最大传输单元 (MTU) 大小。 |
| UINT32 | 适配器多播的列表的大小。 |
| UINT16 | 回填大小 （字节）。 此值不能超过 256 个字节。 |
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 适配器的永久 MAC 地址。 如果设备支持多个永久 MAC 地址，则应返回将由设备的第一个 MAC 地址。 |
| UINT32 | 支持的最大以 kbps 为单位的此适配器的发送速率。 |
| UINT32 | 支持的最大接收此适配器的速率，以 kbps 为单位。 |
| UINT8 | 指定是否由硬件启用单选。 有效值为 0 （禁用） 和 1 （启用）。 |
| UINT8 | 指定是否它们单选启用的软件。 有效值为 0 （禁用） 和 1 （启用）。 |
| UINT8 | 指定接口是否支持 PLR。 有效值为 0 （不支持） 和 1 （支持）。 |
| UINT8 | 指定接口是否支持 FLR。 有效值为 0 （不支持） 和 1 （支持）。 |
| UINT8 | 指定是否支持发送和接收操作帧。 有效值为 0 （不支持） 和 1 （支持）。 |
| UINT8 | RX 空间流的支持的数目。 |
| UINT8 | TX 空间流的支持的数目。 |
| UINT8 | 适配器可以同时处理，而不考虑操作模式的通道数。 |
| UINT8 | 指定是否支持天线多样性。 有效值为 0 （不支持） 和 1 （支持）。 |
| UINT8 | 指定是否支持 eCSA。 有效值为 0 （不支持） 和 1 （支持）。 |
| UINT8 | 指定适配器是否支持 MAC 地址随机化。 有效值为 0 （不支持） 和 1 （支持）。 |
 | [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 为每个地址位可以是随机的 (0) 还是应保留为永久地址 (1) 相同的值指定一个位掩码。 默认值为全部为零。 |
| [**WDI\_蓝牙\_共存\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_bluetooth_coexistence_support) (UINT32) | Wi-fi-蓝牙共存的受支持的级别。 |
| UINT8 | 指定非 WDI OID 的支持。 有效值包括： <ul><li>0 :不支持。 Microsoft 组件并不了解不转发到适配器的 Oid。</li><li>1 :支持。 Microsoft 组件不能理解转发到适配器的 Oid。</li></ul> <p>这些 Oid 将不包含 WDI 标头。 若要标识该请求来自的适配器的端口，请使用**NdisPortNumber**在 NDIS\_OID\_请求并将它匹配中的一个[WDI\_任务\_创建\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)。</p> |
| UINT8 | 指定是否支持快速转换。 有效值为 0 （不支持） 和 1 （支持）。 |
| UINT8 | 指定是否支持 Mu MIMO。 有效值为 0 （不支持） 和 1 （支持）。 |
| UINT8 | 指定此接口不能支持 Miracast 的接收器。 有效值为 0 （支持） 和 1 （不支持）。 |
| UINT8 | 指定如果 802.11v BSS 转换支持。 有效值为 0 （不支持） 和 1 （支持）。 |
| UINT8 |  指定设备是否支持 IP 停靠功能。 有效值为 0 （不支持） 和 1 （支持）。 <p>在 Windows 10，版本 1607，WDI 版本 1.0.21 中添加。</p> |
| UINT8 | 指定设备是否支持 SAE 身份验证。 有效值为 0 （不支持） 和 1 （支持）。 <p>在 Windows 10，版本 1903，WDI 版本 1.1.8 中添加。</p> |
| UINT8 | 指定设备是否支持 Multiband 操作 (MBO)。 有效值为 0 （不支持） 和 1 （支持）。 <p>在 Windows 10，版本 1903，WDI 版本 1.1.8 中添加。</p> |
| UINT8 | 指定是否适配器实现信号报表度量值。 有效值为的 0 （适配器未实现信号报表度量值） 和 1 （适配器实现其自己 11 k 信号报表）。 <p>在 Windows 10，版本 1903，WDI 版本 1.1.8 中添加。</p> |

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

 

 




