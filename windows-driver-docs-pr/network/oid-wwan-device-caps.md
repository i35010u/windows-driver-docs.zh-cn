---
title: OID_WWAN_DEVICE_CAPS
description: OID_WWAN_DEVICE_CAPS 返回 MB 设备的功能，包括它支持的移动电话技术、它支持的数据包数据的类、它支持的射频类型、它所提供的语音服务的类型以及它是否使用订户标识模块 (SIM 卡) 。 受支持的移动电话技术以及设备是否使用 SIM 尤为重要，因为网络提供程序选择和 SIM 用户界面取决于这两项功能的值。 制造商和固件版本作为可选字段返回。 不支持设置请求。 微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，稍后发送 NDIS_STATUS_WWAN_DEVICE_CAPS 状态通知，其中包含一个 NDIS_WWAN_DEVICE_CAPS 结构，该通知指示完成查询请求时的 MB 设备功能。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_CAPS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 00dc557a6d7f5916a16f4d7553ebdd0d07d2636b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797963"
---
# <a name="oid_wwan_device_caps"></a>OID \_ WWAN \_ 设备 \_ CAP


OID \_ WWAN \_ 设备 \_ cap 返回 MB 设备的功能，包括它支持的移动电话技术、它支持的数据包数据的类、它支持的射频类型、它所提供的语音服务的类型，以及是否使用订户标识模块 (SIM 卡) 。 受支持的移动电话技术以及设备是否使用 SIM 尤为重要，因为网络提供程序选择和 SIM 用户界面取决于这两项功能的值。 制造商和固件版本作为可选字段返回。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，并在以后发送 [**ndis \_ 状态 \_ WWAN \_ 设备 \_ cap**](./ndis-status-wwan-device-caps.md) 状态通知，其中包含 [**ndis \_ WWAN \_ 设备 \_**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps) cap 结构，该通知在完成查询请求时指示 MB 设备的功能。

<a name="remarks"></a>备注
-------

从 Windows 8 开始，MB 驱动程序模型已更新到版本2.0。 Windows 8 微型端口驱动程序应将 [**ndis \_ wwan \_ 设备 \_ Cap**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)结构的 **标头. 修订** 成员设置为 *查询* 请求的 **ndis \_ wwan \_ 设备 \_ cap \_ 版本 \_ 2** 。 Windows 7 微型端口驱动程序应将 **ndis \_ wwan \_ 设备 \_ Cap** 结构的 "**修订** 成员" 成员设置为 "用于 *查询* 请求的 **ndis \_ wwan \_ 设备 \_ cap \_ 版本 \_ 1** "。

有关使用此 OID 的详细信息，请参阅 [WWAN 驱动程序初始化过程](./mb-miniport-driver-initialization.md)。

当处理查询操作时，微型端口驱动程序可以访问设备内存，但不应访问提供程序网络或订阅服务器标识模块 (SIM 卡) 。

如今，许多 "世界范围" MB 设备支持多个频率区段，因为 2.5 G/3G 的频带大小因国家/地区而异。 下表显示了在基于 GSM 的网络的3GPP 标准 (中指定的所有射频频率的列表) 和基于 CDMA 的网络的3GPP2 标准 () 。 这两个标准采用类似的带区分类方案。

**3GPP (基于 GSM 的) 频段类**

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th>3GPP 带区</th>
<th>指定色谱</th>
<th>行业名称</th>
<th>上行 (MS 到 BTS) </th>
<th>下行 (BTS 到 MS) </th>
<th>区域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>带 I</p></td>
<td><p>UMTS2100</p></td>
<td><p>IMT</p></td>
<td><p>1920-1980</p></td>
<td><p>2110-2170</p></td>
<td><p>欧洲、韩国、日本、中国</p></td>
</tr>
<tr class="even">
<td><p>区段 II</p></td>
<td><p>UMTS1900</p></td>
<td><p>PCS1900</p></td>
<td><p>1850-1910</p></td>
<td><p>1930-1990</p></td>
<td><p>北美，LATAM</p></td>
</tr>
<tr class="odd">
<td><p>波段 III</p></td>
<td><p>UMTS1800</p></td>
<td><p>DCS1800</p></td>
<td><p>1710-1785</p></td>
<td><p>1805-1880</p></td>
<td><p>欧洲、中国</p></td>
</tr>
<tr class="even">
<td><p>区段 IV</p></td>
<td><p>AWS</p></td>
<td><p>AWS、1.7/2。1</p></td>
<td><p>1710-1755</p></td>
<td><p>2110-2155</p></td>
<td><p>北美，LATAM</p></td>
</tr>
<tr class="odd">
<td><p>波段 V</p></td>
<td><p>UMTS850</p></td>
<td><p>GSM850</p></td>
<td><p>824-849</p></td>
<td><p>869-894</p></td>
<td><p>北美，LATAM</p></td>
</tr>
<tr class="even">
<td><p>区段 VI</p></td>
<td><p>UMTS800</p></td>
<td><p>UMTS800</p></td>
<td><p>830-840</p></td>
<td><p>875-885</p></td>
<td><p>日本</p></td>
</tr>
<tr class="odd">
<td><p>带 VII</p></td>
<td><p>UMTS2600</p></td>
<td><p>UMTS2600</p></td>
<td><p>2500-2570</p></td>
<td><p>2620-2690</p></td>
<td><p>欧洲</p></td>
</tr>
<tr class="even">
<td><p>带 VIII</p></td>
<td><p>UMTS900</p></td>
<td><p>EGSM900</p></td>
<td><p>880-915</p></td>
<td><p>925-960</p></td>
<td><p>欧洲、中国</p></td>
</tr>
<tr class="odd">
<td><p>带 IX</p></td>
<td><p>UMTS1700</p></td>
<td><p>UMTS1700</p></td>
<td><p>1750-1785</p></td>
<td><p>1845-1880</p></td>
<td><p>日本</p></td>
</tr>
<tr class="even">
<td><p>波段 X</p></td>
<td></td>
<td></td>
<td><p>1710-1770</p></td>
<td><p>2110-2170</p></td>
<td></td>
</tr>
</tbody>
</table>

 

**基于 3GPP2 (CDMA) 频段类**

3GPP 带行业名称上行 (MS 到 BTS) 下行 (BTS 到 MS) 波段0

800MHz 移动电话

824.025-844.995

869.025-889.995

带 I

1900MHz 带区

1850-1910

1930-1990

区段 II

TACS 带区

872.025-914.9875

917.0125-959.9875

波段 III

JTACS 带区

887.0125-924.9875

832.0125-869.9875

区段 IV

韩国 PC 波段

1750-1780

1840-1870

波段 V

450 MHz 带区

410-483.475

420-493.475

区段 VI

2 GHz 波段

1920-1979.950

2110-2169.950

带 VII

700 MHz 带区

776-794

746-764

带 VIII

1800 MHz 带区

1710-1784.950

1805-1879.95

带 IX

900 MHz 带区

880-914.950

925-959.950

波段 X

辅助 800 MHz 带区

806-900.975

851-939.975

波段 XI

400 MHz 欧洲 PAMR

410-483.475

420-493.475

带 I.XII。

800 MHz PAMR

870.125-875.9875

915.0125-920.9875

带 XIII

2.5 GHz IMT2000 扩展带区

2500-2570

2620-2690

乐队 XIV

美国电脑 1.9 GHz 波段

1850-1915

1930-1995

带 XV

AWS 带区

1710-1755

2110-2155

带 XVI

美国 2.5 GHz 波段

2502-2568

2624-2690

带 XVII

仅限美国 2.5 GHz 前向链接波段

2624-2690

 

这两个表中的无线电频率带区的单位为兆赫 (MHz) 。

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

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ 设备 \_ CAP**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)

[WWAN 驱动程序初始化过程](./mb-miniport-driver-initialization.md)

 

