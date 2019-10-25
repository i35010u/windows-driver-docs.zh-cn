---
title: OID_WWAN_DEVICE_CAPS
description: OID_WWAN_DEVICE_CAPS 返回 MB 设备的功能，包括它支持的移动电话技术、它支持的数据包数据类、它支持的射频类型、提供的语音服务的类型以及是否使用订阅者标识模块（SIM 卡）。 受支持的移动电话技术以及设备是否使用 SIM 尤为重要，因为网络提供程序选择和 SIM 用户界面取决于这两项功能的值。 制造商和固件版本作为可选字段返回。 不支持设置请求。 微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，稍后发送 NDIS_STATUS_WWAN_DEVICE_CAPS 状态通知，其中包含 NDIS_WWAN_DEVICE_CAPS结构，该结构指示在完成查询请求时 MB 设备的功能。
ms.assetid: bcf04d0b-70f3-48b7-a505-c82e50edadb2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_CAPS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 47da6d6fb38509d23ba6568bda6e823db1e449f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843862"
---
# <a name="oid_wwan_device_caps"></a>OID\_WWAN\_设备\_CAP


OID\_WWAN\_设备\_CAP 返回 MB 设备的功能，包括它支持的移动电话技术、它支持的数据包数据的类、它支持的广播频率、它所提供的语音服务的类型，以及它是否使用订户标识模块（SIM 卡）。 受支持的移动电话技术以及设备是否使用 SIM 尤为重要，因为网络提供程序选择和 SIM 用户界面取决于这两项功能的值。 制造商和固件版本作为可选字段返回。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后将[**ndis\_状态\_WWAN\_设备发送\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)状态通知，其中包含[**NDIS\_WWAN\_设备\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)结构，该结构指示在完成查询请求时 MB 设备的功能。

<a name="remarks"></a>备注
-------

从 Windows 8 开始，MB 驱动程序模型已更新到版本2.0。 Windows 8 微型端口驱动程序应将[**ndis\_wwan\_设备\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps) **结构的 ndis 成员设置**为**ndis\_WWAN\_设备\_cap**\_*查询*请求。 Windows 7 微型端口驱动程序应将**ndis\_wwan\_设备\_cap** **结构的 ndis 成员设置**为**ndis\_WWAN\_设备\_cap\_1** *查询*请求。

有关使用此 OID 的详细信息，请参阅[WWAN 驱动程序初始化过程](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)。

当处理查询操作时，微型端口驱动程序可以访问设备内存，但不应访问提供程序网络或订阅服务器标识模块（SIM 卡）。

如今，许多 "世界范围" MB 设备支持多个频率区段，因为 2.5 G/3G 的频带大小因国家/地区而异。 下表显示了3GPP 标准（适用于基于 GSM 的网络）和3GPP2 标准（适用于基于 CDMA 的网络）中指定的所有射频频率列表。 这两个标准采用类似的带区分类方案。

**3GPP （基于 GSM）频段类**

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
<th>上行（MS 到 BTS）</th>
<th>下行（BTS 到 MS）</th>
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

 

**3GPP2 （基于 CDMA）频段类**

3GPP 带行业名称上行（MS 到 BTS）下行（BTS 到 MS）波段0

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

 

两个表中的无线电射频带区的单位为兆赫（MHz）。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_设备\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)

[WWAN 驱动程序初始化过程](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)

 

 




