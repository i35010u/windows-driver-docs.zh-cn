---
title: WIA\_IPS\_送纸器\_控件
description: WIA\_IPS\_送纸器\_控件属性用于配置手动送纸器电机控制。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: CA19D573-B461-4D3E-BE2A-CF350E0FA4EA
keywords:
- WIA_IPS_FEEDER_CONTROL 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_FEEDER_CONTROL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0661a204e988c1c2eaa89ec53064742d977b0df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372747"
---
# <a name="wiaipsfeedercontrol"></a>WIA\_IPS\_送纸器\_控件


**WIA\_IPS\_送纸器\_控制**属性用于配置手动送纸器电机控制。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_送纸器\_控制**属性。

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
<td><p>WIA_FEEDER_CONTROL_AUTO</p></td>
<td><p>设备控制送纸器汽车操作。 启动和停止每个扫描作业送纸器 (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv::drvAcquireItemData</strong> </a>调用)。 如果支持该属性，这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_FEEDER_CONTROL_MANUAL</p></td>
<td><p>应用程序控制送纸器汽车操作。 送纸器是当 WIA 微型驱动程序收到 WIA_COMMAND_START_FEEDER 命令请求时启动和停止 WIA 微型驱动程序收到 WIA_COMMAND_STOP_FEEDER 命令请求。</p></td>
</tr>
</tbody>
</table>

 

如果设备支持此功能，WIA 应用程序可用于执行第一个扫描作业之前启动的送纸器马达 (第一个**IWiaTransfer::Download**调用) 和最后一个扫描作业之后停止送纸器 (上一次**IWiaTransfer::Download**调用当前 WIA 应用程序会话中) 已完成。 单个作业之间 (**IWiaTransfer::Download**调用)，送纸器保留其运行速度，并已准备好继续执行下一步作业，而不会延迟。

如果 WIA 微型驱动程序收到[ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)请求时 WIA\_送纸器\_控制\_手动是设置和而不会收到 WIA\_命令\_启动\_送纸器命令，WIA 微型驱动程序必须还原到 WIA\_送纸器\_命令\_自动执行扫描作业之前。

如果 WIA\_送纸器\_控制\_手动设置和 WIA 微型驱动程序收到[ **IWiaMiniDrv::drvUnInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)请求而不会收到 WIA\_命令\_停止\_送纸器命令，WIA 微型驱动程序必须返回到调用之前停止送纸器。

此属性是仅对送纸器项有效 (WIA\_类别\_送纸器) 和是可选的。

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

 

 





