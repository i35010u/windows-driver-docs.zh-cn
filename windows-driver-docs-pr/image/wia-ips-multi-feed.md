---
title: WIA \_ IPS \_ 多 \_ 源
description: WIA \_ IPS \_ 多 \_ 源属性用于配置当在设备上检测到多个源条件时，wia 微型驱动程序要执行的操作。 WIA 微型驱动程序创建并维护此属性。
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
ms.openlocfilehash: f76324cd732fbbeef6f572b75dd24df52f3ac7cd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185005"
---
# <a name="wia_ips_multi_feed"></a>WIA \_ IPS \_ 多 \_ 源


**Wia \_ IPS \_ 多 \_ 源**属性用于配置当在设备上检测到多个源条件时，wia 微型驱动程序要执行的操作。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 " **WIA \_ IPS \_ 多 \_ 源** " 属性的有效值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
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
<td><p>设备检测多个源，停止扫描，为 <a href="wia-dps-document-handling-status.md" data-raw-source="[&lt;strong&gt;WIA_DPS_DOCUMENT_HANDLING_STATUS&lt;/strong&gt;](wia-dps-document-handling-status.md)"><strong>WIA_DPS_DOCUMENT_HANDLING_STATUS</strong></a>设置 MULTIPLE_FEED 位，并将 WIA_ERROR_MULTI_FEED 返回到 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv：:d rvacquireitemdata</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MULTI_FEED_DETECT_STOP_SUCCESS</p></td>
<td><p>设备检测多个源，停止扫描，为 <a href="wia-dps-document-handling-status.md" data-raw-source="[&lt;strong&gt;WIA_DPS_DOCUMENT_HANDLING_STATUS&lt;/strong&gt;](wia-dps-document-handling-status.md)"><strong>WIA_DPS_DOCUMENT_HANDLING_STATUS</strong></a>设置 MULTIPLE_FEED 位， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv：:d rvacquireitemdata</strong></a> 返回，且不会因多源而失败。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MULTI_FEED_DETECT_CONTINUE</p></td>
<td><p>设备检测到多个送纸、发出嘟嘟声或在硬件设备上发出可听见或可见的信号 (建议但不需要) ，然后继续扫描。</p></td>
</tr>
</tbody>
</table>

 

此属性是可选的，仅对作为 WIA 类别送纸器) 在 [**wia \_ IPA \_ 项 \_ 类别**](wia-ipa-item-category.md) 属性中表示的送料器数据源 (项有效 \_ \_ 。

当 WIA 微型驱动程序为 \_ [**WIA \_ DPS \_ 文档 \_ 处理 \_ 状态**](wia-dps-document-handling-status.md) 属性设置多个源位时，微型驱动程序应在微型驱动程序检测到已卸载的进纸器、重新加载或新的扫描作业开始时) 清除此 (位。

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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

