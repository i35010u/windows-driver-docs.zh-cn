---
title: WIA\_IP\_送纸器\_控制
description: WIA\_IP\_进纸器\_控制属性用于配置对进纸器马达的手动控制。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: CA19D573-B461-4D3E-BE2A-CF350E0FA4EA
keywords:
- WIA_IPS_FEEDER_CONTROL 图像设备
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
ms.openlocfilehash: 90823a2c6d171dd154218dac43ea96eb15ee30b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840689"
---
# <a name="wia_ips_feeder_control"></a>WIA\_IP\_送纸器\_控制


**WIA\_ip\_进纸器\_控制**属性用于配置对进纸器马达的手动控制。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT\_I4

有效值： WIA\_的\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了**WIA\_ip\_送纸器\_控制**属性的有效值。

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
<td><p>WIA_FEEDER_CONTROL_AUTO</p></td>
<td><p>设备控制送纸器马达操作。 为每个扫描作业（<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv：:D rvacquireitemdata</strong></a>调用）启动并停止了馈送器。 如果支持该属性，则这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_FEEDER_CONTROL_MANUAL</p></td>
<td><p>应用程序控制送纸器马达操作。 当 wia 微型驱动程序收到 WIA_COMMAND_START_FEEDER 命令请求并在 WIA 微型驱动程序收到 WIA_COMMAND_STOP_FEEDER 命令请求时停止时，将启动该送纸器。</p></td>
</tr>
</tbody>
</table>

 

当设备支持此功能时，WIA 应用程序可使用它在执行第一个扫描作业（第一个**IWiaTransfer：:D o)** 调用）之前启动馈送器马达，并在上次扫描作业（最后一个**IWiaTransfer：:D o)** 当前 WIA 应用程序会话中的调用）已完成。 在单独的作业（**IWiaTransfer：:D o)** 调用）之间，进纸器会保持其运行速度，并已准备好继续下一个作业而无需延迟。

如果 wia 微型驱动程序在 WIA\_进纸器\_控制\_rvAcquireItemData 时收到[**IWiaMiniDrv：:D**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)请求，但未接收 WIA\_命令\_启动\_进纸器命令，WIA在执行扫描作业之前，微型驱动程序必须还原为 WIA\_送纸器\_命令\_自动执行。

如果 WIA\_送纸器\_控制\_"手动"，并且 WIA 微型驱动程序收到[**IWiaMiniDrv：:D rvuninitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)请求，但未接收 WIA\_命令\_"停止\_进纸器命令"，则 WIA 微型驱动程序必须在返回呼叫之前停止进纸器。

此属性仅对 "送纸器" 项（WIA\_类别\_进纸器）有效，它是可选的。

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

 

 





