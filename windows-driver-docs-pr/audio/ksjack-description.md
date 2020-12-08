---
title: KSJACK \_ 说明结构
description: KSJACK \_ 描述结构指定音频插孔的物理属性。
keywords:
- KSJACK_DESCRIPTION 构造音频设备
- PKSJACK_DESCRIPTION 结构指针音频设备
topic_type:
- apiref
api_name:
- KSJACK_DESCRIPTION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93cdbf3f4127b56076cec15d3baabb044e839483
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799191"
---
# <a name="ksjack_description-structure"></a>KSJACK \_ 说明结构


KSJACK \_ 描述结构指定音频插孔的物理属性。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct {
  DWORD              ChannelMapping;
  DWORD              Color;
  EPcxConnectionType ConnectionType;
  EPcxGeoLocation    GeoLocation;
  EPcxGenLocation    GenLocation;
  EPxcPortConnection PortConnection;
  BOOL               IsConnected;
} KSJACK_DESCRIPTION, *PKSJACK_DESCRIPTION;
```

<a name="members"></a>成员
-------

**ChannelMapping**  
指定音频通道到相应扬声器位置的映射。 **ChannelMapping** 是 KSAUDIO \_ 发言人 \_ *XXX* 标志的位掩码 (例如， \_ 前 \_ 向左扬声器 |\_ \_ 在头文件 Ksmedia 中定义的扬声器前右) 。 对于模拟呈现端口， **ChannelMapping** 应为非零值。 若要获取捕获插针或数字呈现 pin，请将此成员设置为0。

> [!NOTE]
> Devicetopology 最初定义 **ChannelMapping** 作为 **EChannelMapping** 类型的枚举。 **EChannelMapping** 枚举已被弃用，并且不再用于 windows Vista 和更高版本的 windows 操作系统中。

 

**颜色**  
指定插孔颜色。 颜色表示为32位 RGB 值，该值通过连接8位蓝色、绿色和红色颜色分量形成。 蓝色组件占用了8个最不重要的位 (bits 0-7) ，绿色分量占用了位8-15，红色组件占用了 bits 16-23。 8个最高有效位为零。 如果插孔颜色未知或物理连接器没有可识别的颜色，则该成员的值为0x00000000，表示黑色。

**ConnectionType**  
指定此插孔的物理连接类型。 此成员的值是下表中显示的 **EPcxConnectionType** 枚举值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">连接器类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eConnTypeUnknown</p></td>
<td align="left"><p>未知</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnType3Point5mm</p></td>
<td align="left"><p>3.5 mm minijack</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeQuarter</p></td>
<td align="left"><p>1/4 英寸插座</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeAtapiInternal</p></td>
<td align="left"><p>ATAPI 内部连接器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeRCA</p></td>
<td align="left"><p>RCA 插座</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeOptical</p></td>
<td align="left"><p>光学连接器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeOtherDigital</p></td>
<td align="left"><p>通用数字连接器</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeOtherAnalog</p></td>
<td align="left"><p>一般模拟连接器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeMultichannelAnalogDIN</p></td>
<td align="left"><p>多通道模拟通道连接器</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeXlrProfessional</p></td>
<td align="left"><p>XLR 连接器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeRJ11Modem</p></td>
<td align="left"><p>RJ11 调制解调器连接器</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeCombination</p></td>
<td align="left"><p>连接符组合</p></td>
</tr>
</tbody>
</table>

 

**地理**  
插孔的几何位置。 此成员的值是下表中显示的 **EPcxGeoLocation** 枚举值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">几何位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eGeoLocRear</p></td>
<td align="left"><p>Rear</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocFront</p></td>
<td align="left"><p>Front</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocLeft</p></td>
<td align="left"><p>Left</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocRight</p></td>
<td align="left"><p>Right</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocTop</p></td>
<td align="left"><p>顶部</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocBottom</p></td>
<td align="left"><p>下</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocRearPanel</p></td>
<td align="left"><p>后滑动-打开或请求打开面板</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocRiser</p></td>
<td align="left"><p>转接卡</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocInsideMobileLid</p></td>
<td align="left"><p>移动计算机的内盖</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocDrivebay</p></td>
<td align="left"><p>驱动器托架</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocHDMI</p></td>
<td align="left"><p>HDMI 连接器</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocOutsideMobileLid</p></td>
<td align="left"><p>移动计算机外盖</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocATAPI</p></td>
<td align="left"><p>ATAPI 连接器</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocNotApplicable</p></td>
<td align="left"><p>不适用。 请参阅 <strong>备注</strong> 部分。</p></td>
</tr>
</tbody>
</table>

 

**GenLocation**  
指定插孔的一般位置。 此成员的值是下表中显示的 **EPcxGenLocation** 枚举值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">常规位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eGenLocPrimaryBox</p></td>
<td align="left"><p>在主机箱上</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGenLocInternal</p></td>
<td align="left"><p>主机箱内部</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGenLocSeparate</p></td>
<td align="left"><p>在单独的底盘上</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGenLocOther</p></td>
<td align="left"><p>其他位置</p></td>
</tr>
</tbody>
</table>

 

**PortConnection**  
指定由插座表示的端口类型。 此成员的值是下表中显示的 **EPxcPortConnection** 枚举值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">端口连接类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ePortConnJack</p></td>
<td align="left"><p>插孔</p></td>
</tr>
<tr class="even">
<td align="left"><p>ePortConnIntegratedDevice</p></td>
<td align="left"><p>集成设备的槽</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ePortConnBothIntegratedAndJack</p></td>
<td align="left"><p>集成设备的插孔和槽</p></td>
</tr>
<tr class="even">
<td align="left"><p>ePortConnUnknown</p></td>
<td align="left"><p>未知</p></td>
</tr>
</tbody>
</table>

 

**Connectionmultiplexer.isconnected**  
指示是否有外部设备连接到插孔。 如果音频控制器在此 pin 上支持插座检测，则 **connectionmultiplexer.isconnected** 的值应准确指出插孔是否在任何给定时间都被插头占用。 对于不支持插座检测的设备，此值应始终设置为 **TRUE** 。

<a name="remarks"></a>备注
-------

此结构由 Windows Vista 和更高版本中的 [**KSPROPERTY \_ 插座 \_ 说明**](ksproperty-jack-description.md) 属性使用。 它描述了音频插孔，它是终结点设备与音频适配器中硬件设备之间的连接的一部分。 如果用户需要将终结点设备插入插孔，或将其从插孔中拔出，则音频应用程序可以使用结构中的描述性信息来帮助用户查找插孔。

当音频设备不公开可物理访问的插孔时，音频设备将使用 **eGeoLocNotApplicable** 值向 windows 和基于 windows 的应用程序指示没有物理插孔。 同样，也没有几何位置。 例如，音频设备可以集成到主板中，无需任何可访问的插座。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY \_ 插孔 \_ 说明**](ksproperty-jack-description.md)

 

 






