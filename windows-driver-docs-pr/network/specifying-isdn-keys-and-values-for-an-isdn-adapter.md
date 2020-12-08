---
title: 指定 ISDN 适配器的 ISDN 键和值
description: 指定 ISDN 适配器的 ISDN 键和值
keywords:
- 添加-注册表-每节 WDK 网络，ISDN 适配器
- ISDN 适配器 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b7d4b90cc87a4c83a7c9c06d64f4f99b01156c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834335"
---
# <a name="specifying-isdn-keys-and-values-for-an-isdn-adapter"></a>指定 ISDN 适配器的 ISDN 键和值





除了 **WanEndpoints** 值以外，ISDN 适配器的 INF 文件还必须通过 " *添加注册表" 部分* 添加 (，) 以下项和值添加到适配器的实例键。 有关详细信息，请参阅为 [Wan 适配器指定 Wan 终结点](specifying-wan-endpoints-for-a-wan-adapter.md)。

**注意**   Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用 ISDN 驱动程序。



-   **IsdnNumDChannels**

    指定 ISDN 适配器支持的 D 通道数。

-   **IsdnAutoSwitchDetect** (可选) 

    指定 ISDN 适配器是否支持自动交换机检测。 如果值为1，则表示适配器支持自动交换机检测。 如果值为零，则表示适配器不支持自动交换机检测。

-   **IsdnSwitchTypes**

    指定 ISDN 适配器支持的开关类型。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">开关</th>
    <th align="left">说明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_AUTO</p></td>
    <td align="left"><p>仅北美自动检测 () </p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_ATT</p></td>
    <td align="left"><p>ESS5 (在&T，北美) </p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_NI1</p></td>
    <td align="left"><p>国内 ISDN 1 (NI-1) </p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_NI2</p></td>
    <td align="left"><p>国内 ISDN 2 (NI-2) </p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_NT1</p></td>
    <td align="left"><p>北电信 DMS 100 (NT-1) </p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_INS64</p></td>
    <td align="left"><p>NTT INS64 (日本) </p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_1TR6</p></td>
    <td align="left"><p>德国国家 (1TR6) 。 此开关类型很少使用。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_VN3</p></td>
    <td align="left"><p>法国国家 (VN3) 。 此开关类型很少使用。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_NET3</p></td>
    <td align="left"><p>欧洲 ISDN (DSS1) </p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_DSS1</p></td>
    <td align="left"><p>欧洲 ISDN (DSS1) </p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_AUS</p></td>
    <td align="left"><p>澳大利亚国家标准。 此开关类型很少使用。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_BEL</p></td>
    <td align="left"><p>比利时国。 此开关类型很少使用。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_VN4</p></td>
    <td align="left"><p>法国国家 (VN4) </p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_SWE</p></td>
    <td align="left"><p>瑞典语</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_ITA</p></td>
    <td align="left"><p>意大利国</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_TWN</p></td>
    <td align="left"><p>闽南</p></td>
    </tr>
    </tbody>
    </table>




若要指定多个交换机类型，只需将各个交换机类型值一起添加。

ISDN 向导在安装 ISDN 组件期间自动运行，使用户能够选择 **IsdnSwitchTypes** 指定的一种交换机类型。 所选交换机类型决定了 ISDN 向导随后为配置显示的其他 ISDN 参数。 这些 ISDN 参数包括电话号码、SPID (服务配置文件标识符) 、子地址和 multisubscriber 号码。


-   每个 D 通道的 **IsdnNumBChannels** 值和 *d 通道* 键

    *D 信道* 键是从0到9的从零开始的索引，用于标识 D 通道。 **IsdnNumBChannels** 是 \_ 添加到 *D 通道* 键的注册表 DWORD 值。 **IsdnNumBChannels** 指定 D 通道支持的 B 通道数。

下面是一个 " *添加注册表" 部分* 的示例，它将 isdn 密钥和值添加到 isdn 适配器的实例密钥中。 为适配器指定两个 D 通道，并为每个 D 通道指定两个 B 通道。

```INF
[ISDNadapter.reg]
HKR,,  WanEndPoints,         0x00010001, 4
HKR,,  IsdnNumDChannels,     0x00010001, 2
HKR,,  IsdnAutoSwitchDetect, 0x00010001, 1
HKR,,  IsdnSwitchTypes,      0x00010001, 0x00000004  ;NI1

HKR, 0, IsdnNumBChannels,    0x00010001, 2

HKR, 1, IsdnNumBChannels,    0x00010001, 2
```

ISDN 向导本身还会根据用户指定的参数值，将 ISDN 密钥和值添加到 ISDN 适配器的实例密钥中。 ISDN 向导将添加以下键和值：

-   **IsdnSwitchType**

    \_指示用户为 ISDN 适配器选择的开关类型的注册表 DWORD。

-   每个 D 通道的 **IsdnMultiSubscriberNumbers** 值

    一个 REG \_ 多 \_ SZ 值，指示用户为 D 通道指定的 multisubscriber 编号。

-   *B 通道* 密钥和每个 b 通道的 **IsdnSpid**、 **IsdnPhoneNumber** 和/或 **IsdnSubaddress** 值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">键或值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>B 通道</em> 键</p></td>
<td align="left"><p>标识 B 通道的从零开始的索引。 <em>B 通道</em>键的最大值是一小于分配给 B 通道所属 D 通道的<strong>IsdnNumBchannels</strong>值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IsdnSpid</strong></p></td>
<td align="left"><p>一个 REG_SZ 值，该值指示用户为 B 通道指定的 SPID （如果有）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IsdnPhoneNumber</strong></p></td>
<td align="left"><p>用户为 B 通道指定的电话号码（如果有）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IsdnSubaddress</strong></p></td>
<td align="left"><p>用户为 B 通道指定的子地址（如果有）。</p></td>
</tr>
</tbody>
</table>



以下示例是 ISDN 适配器的注册表部分布局。 每个注册表项都用方括号括起来，例如： \[ *KeyName* \] 。 ISDN 适配器的 INF 文件添加的 ISDN 密钥和值以粗体文本突出显示;ISDN 向导添加的 ISDN 密钥和值以普通 (nonboldface) 文本显示。

```INF
[...Enum\emumeratorID\device-instance-id]  ;ISDN adapter instance key
WanEndpoints=4
IsdnNumDChannels=2
IsdnAutoSwitchDetect=1
IsdnSwitchType=0x4  ;National ISDN 1

[...Enum\emumeratorID\device-instance-id\0]  ;D-channel 0
IsdnNumBChannels=2
IsdnMultiSubscriberNumbers=1234567 2345678 3456789

[...Enum\emumeratorID\device-instance-id\0\0]  ;B-channel 0 for D-channel 0
IsdnSpid=00555121200
IsdnPhoneNumber=5551212
IsdnSubaddress=

[...Enum\emumeratorID\device-instance-id\0\1]  ;B-channel 1 key for D-channel 0
IsdnSpid=00555121300
IsdnPhoneNumber=5551213
IsdnSubaddress=

[...Enum\emumeratorID\device-instance-id\1]  ;D-channel 1 key
IsdnNumBChannels=2
IsdnMultiSubscriberNumbers=8675309 2390125 7658156

[...Enum\emumeratorID\device-instance-id\1\0]  ;B-channel 0 for D-channel 1
IsdnSpid=00555987600
IsdnPhoneNumber=5559876
IsdnSubaddress=

[...Enum\emumeratorID\device-instance-id\1\0]  ;B-channel 1 for D-channel 1
IsdnSpid=00555876500
IsdnPhoneNumber=5558765
IsdnSubaddress=
```









