---
title: OID_WWAN_DEVICE_CAPS
description: OID_WWAN_DEVICE_CAPS 返回 MB 设备的功能，包括移动电话技术支持，它支持的数据包数据，它支持无线电频率、 语音服务，它提供的类型的类以及其是否使用订阅服务器识别模块 （SIM 卡）。 受支持的移动电话技术和设备是否使用 SIM 是特别重要，因为网络提供程序选择和 SIM 用户界面取决于这两项功能的值。 作为可选字段返回的制造商和固件修订版本。 不支持组的请求。 微型端口驱动程序必须查询请求进行异步处理，最初将 NDIS_STATUS_INDICATION_REQUIRED 恢复到原始请求，并更高版本发送包含 NDIS_WWAN_DEVICE_CAPS NDIS_STATUS_WWAN_DEVICE_CAPS 状态通知结构，它指示完成查询请求时的 MB 设备的功能。
ms.assetid: bcf04d0b-70f3-48b7-a505-c82e50edadb2
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_CAPS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cece38d740ade8029b242ebc9adb434dbdce09a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362851"
---
# <a name="oidwwandevicecaps"></a>OID\_WWAN\_DEVICE\_CAPS


OID\_WWAN\_设备\_CAPS 返回 MB 设备，包括它支持的移动电话技术的功能，它支持的数据包数据，它支持无线电频率、 语音的类型的类的维护提供了，以及其是否使用用户识别模块 （SIM 卡）。 受支持的移动电话技术和设备是否使用 SIM 是特别重要，因为网络提供程序选择和 SIM 用户界面取决于这两项功能的值。 作为可选字段返回的制造商和固件修订版本。

不支持组的请求。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_设备\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)状态通知包含[ **NDIS\_WWAN\_设备\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)结构，完成查询请求时指示 MB 设备的功能。

<a name="remarks"></a>备注
-------

从 Windows 8 开始，MB 驱动程序模型已更新为版本 2.0。 Windows 8 微型端口驱动程序应设置**Header.Revision**的成员[ **NDIS\_WWAN\_设备\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)结构**NDIS\_WWAN\_设备\_CAPS\_修订\_2**对于*查询*请求。 Windows 7 微型端口驱动程序应设置**Header.Revision**的成员**NDIS\_WWAN\_设备\_CAPS**结构**NDIS\_WWAN\_设备\_CAPS\_修订\_1**有关*查询*请求。

有关使用此 OID 的详细信息，请参阅[WWAN 驱动程序初始化过程](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)。

当处理查询操作，但不是能访问提供程序网络或用户识别模块 （SIM 卡） 时，微型端口驱动程序可以访问设备的内存。

多个"全球范围内"MB 设备现在支持多个频率带区，因为频率带区为 2.5 g / 3 G 不同国家/地区到国家/地区。 所有 3GPP 标准 （适用于基于 GSM 的网络） 和 （适用于基于 CDMA 的网络） 3GPP2 标准中指定的射频显示下表中的列表。 这两种标准采用类似的带区分类方案。

**3GPP （基于 GSM） 频率外类**

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
<th>3GPP 外</th>
<th>指定的范围</th>
<th>行业名称</th>
<th>上行链路 （BTS 到毫秒）</th>
<th>下行链路 (BTS 到毫秒)</th>
<th>Regions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>我外</p></td>
<td><p>UMTS2100</p></td>
<td><p>IMT</p></td>
<td><p>1920-1980</p></td>
<td><p>2110-2170</p></td>
<td><p>欧洲、 韩国、 日本、 中国</p></td>
</tr>
<tr class="even">
<td><p>带外 II</p></td>
<td><p>UMTS1900</p></td>
<td><p>PCS1900</p></td>
<td><p>1850-1910</p></td>
<td><p>1930-1990</p></td>
<td><p>North America、 LATAM</p></td>
</tr>
<tr class="odd">
<td><p>带外 III</p></td>
<td><p>UMTS1800</p></td>
<td><p>DCS1800</p></td>
<td><p>1710-1785</p></td>
<td><p>1805-1880</p></td>
<td><p>欧洲中国</p></td>
</tr>
<tr class="even">
<td><p>带外 IV</p></td>
<td><p>AWS</p></td>
<td><p>AWS, 1.7/2.1</p></td>
<td><p>1710-1755</p></td>
<td><p>2110-2155</p></td>
<td><p>North America、 LATAM</p></td>
</tr>
<tr class="odd">
<td><p>带外 V</p></td>
<td><p>UMTS850</p></td>
<td><p>GSM850</p></td>
<td><p>824-849</p></td>
<td><p>869-894</p></td>
<td><p>North America、 LATAM</p></td>
</tr>
<tr class="even">
<td><p>带外 VI</p></td>
<td><p>UMTS800</p></td>
<td><p>UMTS800</p></td>
<td><p>830-840</p></td>
<td><p>875-885</p></td>
<td><p>日本</p></td>
</tr>
<tr class="odd">
<td><p>带外 VII</p></td>
<td><p>UMTS2600</p></td>
<td><p>UMTS2600</p></td>
<td><p>2500-2570</p></td>
<td><p>2620-2690</p></td>
<td><p>欧洲</p></td>
</tr>
<tr class="even">
<td><p>带外 VIII</p></td>
<td><p>UMTS900</p></td>
<td><p>EGSM900</p></td>
<td><p>880-915</p></td>
<td><p>925-960</p></td>
<td><p>欧洲中国</p></td>
</tr>
<tr class="odd">
<td><p>带外 IX</p></td>
<td><p>UMTS1700</p></td>
<td><p>UMTS1700</p></td>
<td><p>1750-1785</p></td>
<td><p>1845-1880</p></td>
<td><p>日本</p></td>
</tr>
<tr class="even">
<td><p>带 X</p></td>
<td></td>
<td></td>
<td><p>1710-1770</p></td>
<td><p>2110-2170</p></td>
<td></td>
</tr>
</tbody>
</table>

 

**3GPP2 （基于 CDMA） 频率外类**

3GPP 外行业名称上行 (MS 到 BTS) 下行链路 (BTS 到毫秒) 外 0

800MHz Cellular

824.025-844.995

869.025-889.995

我外

1900 MHz 外

1850-1910

1930-1990

带外 II

TACS 外

872.025-914.9875

917.0125-959.9875

带外 III

JTACS 外

887.0125-924.9875

832.0125-869.9875

带外 IV

朝鲜语电脑外

1750 - 1780

1840 - 1870

带外 V

450 MHz Band

410 - 483.475

420 - 493.475

带外 VI

2 GHz 外

1920 - 1979.950

2110 - 2169.950

带外 VII

700 MHz Band

776 - 794

746 - 764

带外 VIII

1800 MHz Band

1710 - 1784.950

1805 - 1879.95

带外 IX

900 MHz Band

880 - 914.950

925 - 959.950

带 X

辅助 800 MHz 外

806 - 900.975

851 - 939.975

带外 XI

400 MHz 欧洲 PAMR 外

410 - 483.475

420 - 493.475

带外 XII

800 MHz PAMR 外

870.125 - 875.9875

915.0125 - 920.9875

带外 XIII

2.5 g h z IMT2000 扩展外

2500 - 2570

2620 - 2690

带外 XIV

美国 PC 1.9 GHz 外

1850 - 1915

1930 - 1995

带外 XV

AWS 外

1710 - 1755

2110 - 2155

带外 XVI

美国 2.5ghz 外

2502 - 2568

2624 - 2690

带外 XVII

美国 2.5ghz 前向链接仅外

2624-2690

 

这两个表中的射频带区的单位是兆赫 (MHz)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_DEVICE\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)

[WWAN 驱动程序初始化过程](https://docs.microsoft.com/windows-hardware/drivers/network/mb-miniport-driver-initialization)

 

 




