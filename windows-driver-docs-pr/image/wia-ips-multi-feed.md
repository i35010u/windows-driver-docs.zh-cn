---
title: WIA\_IPS\_多\_源
description: WIA\_IPS\_多\_源属性用于配置要在设备上检测到多个源的条件时由 WIA 微型驱动程序执行的操作。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 8BD92273-218B-4381-BCAF-ED9D227B6B94
keywords:
- WIA_IPS_MULTI_FEED 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MULTI_FEED
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7aa0b980da213adfd84d18afc6c4f9b04cf5300
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348246"
---
# <a name="wiaipsmultifeed"></a>WIA\_IPS\_多\_源


**WIA\_IPS\_多\_馈送**属性用于配置要在设备上检测到多个源的条件时由 WIA 微型驱动程序执行的操作。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_多\_馈送**属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_MULTI_FEED_DETECT_DISABLED</p></td>
<td><p>多源的检测已禁用。 如果支持该属性，这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MULTI_FEED_DETECT_STOP_ERROR</p></td>
<td><p>设备检测到多源、 停止扫描、 设置位 MULTIPLE_FEED <a href="wia-dps-document-handling-status.md" data-raw-source="[&lt;strong&gt;WIA_DPS_DOCUMENT_HANDLING_STATUS&lt;/strong&gt;](wia-dps-document-handling-status.md)"> <strong>WIA_DPS_DOCUMENT_HANDLING_STATUS</strong></a>，并返回到 WIA_ERROR_MULTI_FEED <a href="https://msdn.microsoft.com/library/windows/hardware/ff543956" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543956)"> <strong>IWiaMiniDrv::drvAcquireItemData</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MULTI_FEED_DETECT_STOP_SUCCESS</p></td>
<td><p>设备检测到多源、 停止扫描、 设置位 MULTIPLE_FEED <a href="wia-dps-document-handling-status.md" data-raw-source="[&lt;strong&gt;WIA_DPS_DOCUMENT_HANDLING_STATUS&lt;/strong&gt;](wia-dps-document-handling-status.md)"> <strong>WIA_DPS_DOCUMENT_HANDLING_STATUS</strong></a>，并<a href="https://msdn.microsoft.com/library/windows/hardware/ff543956" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543956)"> <strong>IWiaMiniDrv::drvAcquireItemData</strong> </a>返回并不会由于多源失败。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MULTI_FEED_DETECT_CONTINUE</p></td>
<td><p>设备检测多源、 时发出提示音或生成的声音或可见的信号，在硬件设备 （建议但不是必需的），并继续扫描。</p></td>
</tr>
</tbody>
</table>

 

此属性是可选的并且仅对送纸器数据源项有效 (以表示[ **WIA\_IPA\_项\_类别**](wia-ipa-item-category.md)属性作为 WIA\_类别\_送纸器)。

当 WIA 微型驱动程序设置多个\_源位[ **WIA\_DPS\_文档\_处理\_状态**](wia-dps-document-handling-status.md)属性，很快就如微型驱动程序检测到送纸器中卸载，则将重新加载或新扫描作业开始时，微型驱动程序应清除此位 （标志）。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





