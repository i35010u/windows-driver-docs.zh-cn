---
title: WIA \_ IP \_ 进纸器 \_ 控制
description: "\"WIA \\_ ip \\_ 进纸器 \\_ 控制\" 属性用于配置对进纸器马达的手动控制。 WIA 微型驱动程序创建并维护此属性。"
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
ms.openlocfilehash: 20121d7e3d692916616a22fcc2af15965a85d60b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190721"
---
# <a name="wia_ips_feeder_control"></a>WIA \_ IP \_ 进纸器 \_ 控制


" **WIA \_ ip \_ 进纸器 \_ 控制** " 属性用于配置对进纸器马达的手动控制。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>注解
-------

下表描述了 " **WIA \_ ip \_ 进纸器 \_ 控制** " 属性的有效值。

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
<td><p>WIA_FEEDER_CONTROL_AUTO</p></td>
<td><p>设备控制送纸器马达操作。  (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv：:D rvacquireitemdata</strong></a> 调用) ，为每个扫描作业启动和停止了馈送器。 如果支持该属性，则这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_FEEDER_CONTROL_MANUAL</p></td>
<td><p>应用程序控制送纸器马达操作。 当 wia 微型驱动程序收到 WIA_COMMAND_START_FEEDER 命令请求并在 WIA 微型驱动程序接收到 WIA_COMMAND_STOP_FEEDER 命令请求时停止时，将启动该送纸器。</p></td>
</tr>
</tbody>
</table>

 

当设备支持此功能时，WIA 应用程序可以使用它来启动进纸器马达，然后 (第一个 **IWiaTransfer：:D o) ** 调用) ，并在上次扫描作业之后停止进纸器 (当前 WIA 应用程序会话:D 中的最后一个 **IWiaTransfer：) o) ** 调用已完成。 在单独的作业 (**IWiaTransfer：:D o) ** 调用) 时，送纸器会保持其运行速度，并且已准备好继续下一个作业而不延迟。

如果 wia 微型驱动程序在设置了 WIA 进纸器控制手册时接收到 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 请求，但 \_ \_ \_ 未收到 wia \_ 命令 \_ \_ "启动进纸器命令"，则 \_ 在 \_ \_ 执行扫描作业之前，wia 微型驱动程序必须还原为 wia 进纸器命令 "自动"。

如果 \_ 设置了 wia 进纸器 \_ 控制 \_ 手册并且 wia 微型驱动程序接收到 [**IWiaMiniDrv：:d rvuninitializewia**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia) 请求，但未收到 WIA \_ 命令 \_ \_ "停止进纸器" 命令，则 wia 微型驱动程序必须停止进纸器才能返回到呼叫。

此属性仅对 (WIA 类别送纸器) 的进纸器项有效 \_ \_ ，并且是可选的。

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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

