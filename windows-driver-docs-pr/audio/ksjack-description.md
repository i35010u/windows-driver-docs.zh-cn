---
title: KSJACK\_描述结构
description: KSJACK\_描述结构指定的音频插孔的物理属性。
ms.assetid: 303bc73a-fe47-499b-97b3-7c49a40e8cfa
keywords:
- KSJACK_DESCRIPTION 结构音频设备
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
ms.openlocfilehash: e1657777c2466aa50bbbda559ea3f3bb6dd4d09e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333380"
---
# <a name="ksjackdescription-structure"></a>KSJACK\_描述结构


KSJACK\_描述结构指定的音频插孔的物理属性。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct {
  DWORD              ChannelMapping;
  DWORD              Color;
  EPcxConnectionType ConnectionType;
  EPcxGeoLocation    GeoLocation;
  EPcxGenLocation    GenLocation;
  EPxcPortConnection PortConnection;
  BOOL               IsConnected;
} KSJACK_DESCRIPTION, *PKSJACK_DESCRIPTION;
```

<a name="members"></a>成员
-------

**ChannelMapping**  
指定的映射到相应的扬声器位置的音频通道。 **ChannelMapping**是一个位掩码的 KSAUDIO\_演讲者\_*XXX*标志 (例如，说话人\_前端\_左侧 |说话人\_FRONT\_右侧)，该标头文件 Ksmedia.h 中定义。 **ChannelMapping**应为非零值仅用于模拟呈现 pin。 对于捕获 pin 或数字呈现插针，将此成员设置为 0。

&gt; \[!请注意\]&gt;最初定义 Devicetopology.h **ChannelMapping**为枚举的类型**EChannelMapping**。 **EChannelMapping**枚举已被弃用并不再使用 Windows Vista 和更高版本的 Windows 操作系统中。

 

**Color**  
指定 jack 颜色。 颜色表示为一个 32 位 RGB 值，通过串联的 8 位蓝色、 绿色和红色颜色组件。 蓝色组件占用 8 的最低有效位 （0-7 位），绿色分量所占位 8 月 15 日，而红色组件占用位 16-23。 8 的最高有效位均为零。 如果 jack 颜色为未知或物理连接器具有没有可识别的颜色，此成员的值将为 0x00000000，表示黑色。

**ConnectionType**  
为此 jack 指定物理连接类型。 此成员的值是之一**EPcxConnectionType**下表中所示的枚举值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">连接器类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eConnTypeUnknown</p></td>
<td align="left"><p>Unknown</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnType3Point5mm</p></td>
<td align="left"><p>3.5mm 微型插孔</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeQuarter</p></td>
<td align="left"><p>1/4-英寸插孔</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeAtapiInternal</p></td>
<td align="left"><p>ATAPI 内部连接器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeRCA</p></td>
<td align="left"><p>RCA 插孔</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeOptical</p></td>
<td align="left"><p>光学连接器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeOtherDigital</p></td>
<td align="left"><p>泛型数字连接器</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeOtherAnalog</p></td>
<td align="left"><p>泛型模拟连接器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeMultichannelAnalogDIN</p></td>
<td align="left"><p>多渠道模拟 DIN 连接器</p></td>
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
<td align="left"><p>连接器组合</p></td>
</tr>
</tbody>
</table>

 

**GeoLocation**  
Jack 几何位置。 此成员的值是之一**EPcxGeoLocation**下表中所示的枚举值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">几何位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eGeoLocRear</p></td>
<td align="left"><p>后端</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocFront</p></td>
<td align="left"><p>前端</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocLeft</p></td>
<td align="left"><p>向左</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocRight</p></td>
<td align="left"><p>向右</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocTop</p></td>
<td align="left"><p>顶部</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocBottom</p></td>
<td align="left"><p>底部</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocRearPanel</p></td>
<td align="left"><p>后端滑动打开或请求打开面板</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocRiser</p></td>
<td align="left"><p>转接卡</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocInsideMobileLid</p></td>
<td align="left"><p>深入了解盖的移动计算机</p></td>
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
<td align="left"><p>移动计算机的外部合上盖子</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocATAPI</p></td>
<td align="left"><p>ATAPI 连接器</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocNotApplicable</p></td>
<td align="left"><p>不适用。 请参阅<strong>备注</strong>部分。</p></td>
</tr>
</tbody>
</table>

 

**GenLocation**  
指定 jack 的常规位置。 此成员的值是之一**EPcxGenLocation**下表中所示的枚举值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">常规位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eGenLocPrimaryBox</p></td>
<td align="left"><p>在主底盘</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGenLocInternal</p></td>
<td align="left"><p>深入了解主底盘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGenLocSeparate</p></td>
<td align="left"><p>在单独的机箱</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGenLocOther</p></td>
<td align="left"><p>其他位置</p></td>
</tr>
</tbody>
</table>

 

**PortConnection**  
指定表示 jack 端口类型。 此成员的值是之一**EPxcPortConnection**下表中所示的枚举值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">端口连接类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ePortConnJack</p></td>
<td align="left"><p>Jack</p></td>
</tr>
<tr class="even">
<td align="left"><p>ePortConnIntegratedDevice</p></td>
<td align="left"><p>集成的设备的插槽</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ePortConnBothIntegratedAndJack</p></td>
<td align="left"><p>Jack 和集成的设备的插槽</p></td>
</tr>
<tr class="even">
<td align="left"><p>ePortConnUnknown</p></td>
<td align="left"><p>Unknown</p></td>
</tr>
</tbody>
</table>

 

**IsConnected**  
指示是否存在外部设备连接到输入插孔。 音频控制器是否支持此 pin 的值 jack 检测**IsConnected**应准确地指示是否在任何给定时间占用的即插即用插孔。 此值应始终设置为 **，则返回 TRUE**不支持 jack 检测的设备。

<a name="remarks"></a>备注
-------

此结构可供[ **KSPROPERTY\_JACK\_说明**](ksproperty-jack-description.md)属性在 Windows Vista 及更高版本。 它描述了属于终结点设备和音频适配器中的硬件设备之间的连接的音频插孔。 当用户需要将终结点设备插入插孔或拔下插座时，音频应用程序可以使用的描述性信息结构中以帮助用户查找插孔。

音频设备时将音频设备不会公开一个以物理方式访问插孔，使用**eGeoLocNotApplicable**值以指示 Windows 和基于 Windows 的应用不存在任何物理插孔。 在这种情况下，没有任何几何位置或者。 例如，音频设备可以集成到主板，而无需任何可访问的插孔。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY\_JACK\_说明**](ksproperty-jack-description.md)

 

 






