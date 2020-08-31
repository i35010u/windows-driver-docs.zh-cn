---
title: ACPI 键盘快捷方式逻辑
description: ACPI 键盘快捷方式逻辑
ms.assetid: cd62380b-1393-403e-b0e6-c52f60c06936
keywords:
- ACPI 热键 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3fe4ba7c192dbe883d824fbea3e6bc89b7847df
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063192"
---
# <a name="acpi-keyboard-shortcut-logic"></a>ACPI 键盘快捷方式逻辑


从 Windows 7 开始，Ihv 实现基于 ACPI 的 OEM 特定键盘快捷方式。 操作系统不知道这些键盘快捷方式。 在 Windows 7 上，Oem 必须使用 CCD 数据库来存储和应用键盘快捷方式，使操作系统和任何 OEM 应用程序都能识别彼此。

对于在 Windows 7 上运行的驱动程序，调用以下函数的行为发生了变化：

<span id="DxgkDdiNotifyAcpiEvent_and_DxgkDdiRecommendFunctionalVidPn"></span><span id="dxgkddinotifyacpievent_and_dxgkddirecommendfunctionalvidpn"></span><span id="DXGKDDINOTIFYACPIEVENT_AND_DXGKDDIRECOMMENDFUNCTIONALVIDPN"></span>[*DxgkDdiNotifyAcpiEvent*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)和[ *DxgkDdiRecommendFunctionalVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)  
-   如果显示微型端口驱动程序接收到在[*DxgkDdiNotifyAcpiEvent*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event) \_ \_ AcpiFlags 参数中设置了 DXGK ACPI 更改显示模式标志的 DxgkDdiNotifyAcpiEvent 函数的调用，则 call center.dmm 将 \_ \_ 调用[*DxgkDdiRecommendFunctionalVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)函数以获取新的 VidPN，并与当前的客户端 VidPN 进行比较。 *AcpiFlags* 如果两个 VidPNs 的拓扑是相同的，则 CALL CENTER.DMM 不会修改新的 VidPN。 否则，CALL CENTER.DMM 将从 VidPN 中删除模式信息，只保留拓扑，并使 CCD 数据库能够确定给定拓扑的模式。 然后，CALL CENTER.DMM 基于新的 VidPN 设置显示配置。

<span id="D3DKMTInvalidateActiveVidPn"></span><span id="d3dkmtinvalidateactivevidpn"></span><span id="D3DKMTINVALIDATEACTIVEVIDPN"></span>[**D3DKMTInvalidateActiveVidPn**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtinvalidateactivevidpn)  
-   在 Windows Vista 和更高版本中，此函数支持 &lt; DXGKDDI \_ 接口 \_ 版本 WIN7 的显示微型端口驱动程序 \_ 。 函数行为与 Windows Vista 上的行为相同。

-   此功能在 Windows 7 和更高版本中不受支持，适用于版本为 &gt; DXGKDDI \_ 接口 \_ 版本 WIN7 的显示微型端口驱动程序 \_ 。 如果调用，则返回状态代码 " \_ 不支持状态" \_ 。

 

