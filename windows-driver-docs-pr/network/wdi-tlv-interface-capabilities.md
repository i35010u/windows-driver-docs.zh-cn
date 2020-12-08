---
title: WDI_TLV_INTERFACE_CAPABILITIES
description: WDI_TLV_INTERFACE_CAPABILITIES 是包含 Wi-Fi 接口功能的 TLV。
ms.date: 02/14/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_INTERFACE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 325e05ffd2695548217d7ff1c5c1a8d8b07a7501
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803657"
---
# <a name="wdi_tlv_interface_capabilities"></a>WDI \_ TLV \_ 接口 \_ 功能


WDI \_ tlv \_ 接口 \_ 功能是包含 Wi-Fi 接口功能的 tlv。

## <a name="tlv-type"></a>TLV 类型

0xF

## <a name="length"></a>长度

Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型 | 描述 |
| --- | --- |
| UINT32 | 最大传输单位 (MTU) 大小。 |
| UINT32 | 适配器的多播列表大小。 |
| UINT16 | 回填大小（以字节为单位）。 此值不能大于256字节。 |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 适配器的永久 MAC 地址。 如果设备支持多个永久 MAC 地址，则应返回设备使用的第一个 MAC 地址。 |
| UINT32 | 此适配器支持的最大发送速率（以 kbps 为单位）。 |
| UINT32 | 此适配器支持的最大接收速率（kbps）。 |
| UINT8 | 指定是否由硬件启用无线电。 有效值为 0 (禁用)  (启用 1) 。 |
| UINT8 | 指定是否由软件启用它们。 有效值为 0 (禁用)  (启用 1) 。 |
| UINT8 | 指定接口是否支持 PLR。 有效值为 0 (不支持) 和 1 (支持) 。 |
| UINT8 | 指定接口是否支持 FLR。 有效值为 0 (不支持) 和 1 (支持) 。 |
| UINT8 | 指定是否支持发送和接收操作帧。 有效值为 0 (不支持) 和 1 (支持) 。 |
| UINT8 | 支持的 RX 空间流数。 |
| UINT8 | 支持的 TX 空间流的数量。 |
| UINT8 | 适配器可以同时工作的通道数，与操作模式无关。 |
| UINT8 | 指定是否支持天线多样性。 有效值为 0 (不支持) 和 1 (支持) 。 |
| UINT8 | 指定是否支持 eCSA。 有效值为 0 (不支持) 和 1 (支持) 。 |
| UINT8 | 指定适配器是否支持 MAC 地址随机化。 有效值为 0 (不支持) 和 1 (支持) 。 |
 | [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 一个位掩码，指定每个地址位是否可以是随机 (0) ，还是应将与永久地址相同的值 (1) 。 默认值为全零。 |
| [**WDI \_\_ \_ 支持**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bluetooth_coexistence_support) (UINT32) 的蓝牙共存 | 支持的 Wi-Fi 级别-蓝牙共存。 |
| UINT8 | 指定不可 WDI 的 OID 支持。 有效值是： <ul><li>0：不支持。 Microsoft 组件不理解的 Oid 不会转发到适配器。</li><li>1：支持。 Microsoft 组件不理解的 Oid 会转发到适配器。</li></ul> <p>这些 Oid 不包含 WDI 标头。 若要确定请求传入的适配器的端口，请在 NDIS OID 请求中使用 **NdisPortNumber** ， \_ 并将 \_ 其与 [WDI \_ 任务 \_ 创建 \_ 端口](./oid-wdi-task-create-port.md)中的对应项匹配。</p> |
| UINT8 | 指定是否支持快速转换。 有效值为 0 (不支持) 和 1 (支持) 。 |
| UINT8 | 指定是否支持 Mu-MIMO。 有效值为 0 (不支持) 和 1 (支持) 。 |
| UINT8 | 指定接口是否不支持 Miracast 接收器。 有效值为 0 (支持的) 和 1 (不支持) 。 |
| UINT8 | 指定是否支持 802.11 v BSS 转换。 有效值为 0 (不支持) 和 1 (支持) 。 |
| UINT8 |  指定设备是否支持 IP 扩展功能。 有效值为 0 (不支持) 和 1 (支持) 。 <p>已在 Windows 10 版本1607、WDI 版本1.0.21 中添加。</p> |
| UINT8 | 指定设备是否支持 SAE authentication。 有效值为 0 (不支持) 和 1 (支持) 。 <p>已在 Windows 10 版本1903、WDI 版本1.1.8 中添加。</p> |
| UINT8 | 指定设备是否支持 Multiband 操作 (MBO) 。 有效值为 0 (不支持) 和 1 (支持) 。 <p>已在 Windows 10 版本1903、WDI 版本1.1.8 中添加。</p> |
| UINT8 | 指定适配器是否实现信标报告度量。 有效值为 0 (适配器未实现信标报表度量值) 和 1 (适配器实现自己的11k 信标报表) 。 <p>已在 Windows 10 版本1903、WDI 版本1.1.8 中添加。</p> |

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

