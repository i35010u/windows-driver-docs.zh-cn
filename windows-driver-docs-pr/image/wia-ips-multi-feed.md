---
title: WIA\_IP\_多\_源
description: WIA\_IPS\_多\_源属性用于配置当在设备上检测到多个源条件时，WIA 微型驱动程序要执行的操作。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 8BD92273-218B-4381-BCAF-ED9D227B6B94
keywords:
- WIA_IPS_MULTI_FEED 图像设备
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
ms.openlocfilehash: e19f602adf098c3f018b2872d52b245381565fe7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840687"
---
# <a name="wia_ips_multi_feed"></a>WIA\_IP\_多\_源


**Wia\_IPS\_多\_源**属性用于配置当在设备上检测到多个源条件时，WIA 微型驱动程序要执行的操作。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT\_I4

有效值： WIA\_的\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了**WIA\_IPS\_多\_源**属性的有效值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_MULTI_FEED_DETECT_DISABLED</p></td>
<td><p>已禁用多源检测。 如果支持该属性，则这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MULTI_FEED_DETECT_STOP_ERROR</p></td>
<td><p>设备检测多个源，停止扫描，为<a href="wia-dps-document-handling-status.md" data-raw-source="[&lt;strong&gt;WIA_DPS_DOCUMENT_HANDLING_STATUS&lt;/strong&gt;](wia-dps-document-handling-status.md)"><strong>WIA_DPS_DOCUMENT_HANDLING_STATUS</strong></a>设置 MULTIPLE_FEED 位，并将 WIA_ERROR_MULTI_FEED 返回到<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv：:d rvacquireitemdata</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MULTI_FEED_DETECT_STOP_SUCCESS</p></td>
<td><p>设备检测多个源，停止扫描，为<a href="wia-dps-document-handling-status.md" data-raw-source="[&lt;strong&gt;WIA_DPS_DOCUMENT_HANDLING_STATUS&lt;/strong&gt;](wia-dps-document-handling-status.md)"><strong>WIA_DPS_DOCUMENT_HANDLING_STATUS</strong></a>设置 MULTIPLE_FEED 位， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv：:d rvacquireitemdata</strong></a>返回，且不会因多源而失败。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MULTI_FEED_DETECT_CONTINUE</p></td>
<td><p>设备检测到多源、发出嘟嘟声或在硬件设备上发出可听见或可见的信号（建议但不是必需的），并继续扫描。</p></td>
</tr>
</tbody>
</table>

 

此属性是可选的，并且仅对送纸器数据源项有效（在[**wia\_IPA\_项\_CATEGORY**](wia-ipa-item-category.md)属性中表示为 WIA\_类别\_进纸器）。

当 WIA 微型驱动程序为[**WIA\_DPS\_文档\_处理\_状态**](wia-dps-document-handling-status.md)属性设置多个\_源位时，微型驱动程序应在微型驱动程序检测到馈送器已卸载、已重新加载或开始新的扫描作业。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef （包括 Wiadef）</td>
</tr>
</tbody>
</table>

 

 





