---
title: ISDN 适配器的指定 ISDN 键和值
description: ISDN 适配器的指定 ISDN 键和值
ms.assetid: ba2156c1-fb54-4e1e-b0ec-72aa2d950505
keywords:
- 添加注册表部分 WDK 网络、 ISDN 适配器
- ISDN 适配器 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84ccf565d14e9366e84bb020a0035f4cd426f2c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540694"
---
# <a name="specifying-isdn-keys-and-values-for-an-isdn-adapter"></a>ISDN 适配器的指定 ISDN 键和值





除了**WanEndpoints**值，一个 INF 文件对于 ISDN 适配器必须添加 (通过*添加注册表部分*) 以下键和向该适配器的实例键的值。 有关详细信息，请参阅[WAN 适配器指定 WAN 终结点](specifying-wan-endpoints-for-a-wan-adapter.md)。

**请注意**ISDN 驱动程序在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。



-   **IsdnNumDChannels**

    指定支持的 ISDN 适配器的 D 通道数。

-   **IsdnAutoSwitchDetect** （可选）

    指定 ISDN 适配器是否支持自动切换检测。 如果值为 1 指示适配器支持自动切换检测。 零值指示该适配器不支持自动切换检测。

-   **IsdnSwitchTypes**

    指定支持的 ISDN 适配器的交换机类型。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">Switch</th>
    <th align="left">描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_AUTO</p></td>
    <td align="left"><p>自动检测 （仅适用于北美地区）</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_ATT</p></td>
    <td align="left"><p>ESS5 AT 和 T (北美地区）</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_NI1</p></td>
    <td align="left"><p>国家/地区 ISDN 1 (NI-1)</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_NI2</p></td>
    <td align="left"><p>国家/地区 ISDN 2 (NI-2)</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_NT1</p></td>
    <td align="left"><p>北电信 DMS 100 (NT-1)</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_INS64</p></td>
    <td align="left"><p>NTT INS64 （日本）</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_1TR6</p></td>
    <td align="left"><p>正使用德语的国家/地区 (1TR6)。 此交换机类型很少使用。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_VN3</p></td>
    <td align="left"><p>法语的国家/地区 (VN3)。 此交换机类型很少使用。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_NET3</p></td>
    <td align="left"><p>欧洲 ISDN (DSS1)</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_DSS1</p></td>
    <td align="left"><p>欧洲 ISDN (DSS1)</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_AUS</p></td>
    <td align="left"><p>澳大利亚国家/地区。 此交换机类型很少使用。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_BEL</p></td>
    <td align="left"><p>比利时国家/地区。 此交换机类型很少使用。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_VN4</p></td>
    <td align="left"><p>法语的国家/地区 (VN4)</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_SWE</p></td>
    <td align="left"><p>瑞典语国家/地区</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_ITA</p></td>
    <td align="left"><p>意大利语国家/地区</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_TWN</p></td>
    <td align="left"><p>中国台湾</p></td>
    </tr>
    </tbody>
    </table>




若要指定多个交换机类型，只需一起添加单独的交换机类型值。

ISDN 向导中，在 ISDN 组件的安装过程中自动运行，使用户可以选择指定的开关类型之一**IsdnSwitchTypes**。 选择的交换机类型确定哪些其他 ISDN 向导随后将显示配置的 ISDN 参数。 这些 ISDN 参数包括电话号码、 SPID （服务配置文件标识符）、 子地址和多数目。


-   **IsdnNumBChannels**值和一个*D 信道*密钥对每个 D 通道

    *D 信道*键是从 0 到 9，用于标识 D 信道的从零开始索引。 **IsdnNumBChannels**是 REG\_DWORD 值添加到*D 信道*密钥。 **IsdnNumBChannels**指定的 B-D 信道支持的通道数。

以下是一种*添加注册表部分*将 ISDN 键和值添加到 ISDN 适配器的实例键。 两个 D 通道指定的适配器，并为每个 D 通道指定了两个 B 通道。

```INF
[ISDNadapter.reg]
HKR,,  WanEndPoints,         0x00010001, 4
HKR,,  IsdnNumDChannels,     0x00010001, 2
HKR,,  IsdnAutoSwitchDetect, 0x00010001, 1
HKR,,  IsdnSwitchTypes,      0x00010001, 0x00000004  ;NI1

HKR, 0, IsdnNumBChannels,    0x00010001, 2

HKR, 1, IsdnNumBChannels,    0x00010001, 2
```

ISDN 向导本身也将添加到基于用户指定的参数值的 ISDN 适配器的实例键的 ISDN 键和值。 ISDN 向导添加以下键和值：

-   **IsdnSwitchType**

    REG\_dword 值，该值指示用户为 ISDN 适配器选择交换机类型。

-   **IsdnMultiSubscriberNumbers**值为每个 D 通道

    REG\_多\_SZ 值，该值指示多 D 通道由用户指定的数字。

-   一个*B 通道*密钥和一个**IsdnSpid**， **IsdnPhoneNumber**，和/或**IsdnSubaddress**为每个 B 通道值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">项或注册表值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>B 通道</em>密钥</p></td>
<td align="left"><p>一个从零开始的索引，它标识 B 通道。 最大值<em>B 通道</em>密钥是一个不会早于<strong>IsdnNumBchannels</strong>值分配给属于 B 通道 D 信道。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IsdnSpid</strong></p></td>
<td align="left"><p>REG_SZ 值，该值指示 SPID，，指定的任何用户 B 通道。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IsdnPhoneNumber</strong></p></td>
<td align="left"><p>电话号码，如果有的话，用户指定的 B 通道。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IsdnSubaddress</strong></p></td>
<td align="left"><p>子地址，如果有的话，用户指定的 B 通道。</p></td>
</tr>
</tbody>
</table>



下面的示例是 ISDN 适配器的注册表部分布局。 每个注册表项是用方括号括起来，例如：\[ *KeyName* \]。 粗体文本; 突出显示了 ISDN 键和值的 ISDN 适配器的 INF 文件添加ISDN 键和值的已添加的 ISDN 向导出现在普通 (nonboldface) 文本。

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









