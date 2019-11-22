---
title: ACPI 键盘快捷方式逻辑
description: ACPI 键盘快捷方式逻辑
ms.assetid: cd62380b-1393-403e-b0e6-c52f60c06936
keywords:
- ACPI 热键 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62d06b6ede3abdcbf504afe5f0f9238da5b8b540
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839082"
---
# <a name="acpi-keyboard-shortcut-logic"></a>ACPI 键盘快捷方式逻辑


从 Windows 7 开始，Ihv 实现基于 ACPI 的 OEM 特定键盘快捷方式。 操作系统不知道这些键盘快捷方式。 在 Windows 7 上，Oem 必须使用 CCD 数据库来存储和应用键盘快捷方式，使操作系统和任何 OEM 应用程序都能识别彼此。

对于在 Windows 7 上运行的驱动程序，调用以下函数的行为发生了变化：

<span id="DxgkDdiNotifyAcpiEvent_and_DxgkDdiRecommendFunctionalVidPn"></span><span id="dxgkddinotifyacpievent_and_dxgkddirecommendfunctionalvidpn"></span><span id="DXGKDDINOTIFYACPIEVENT_AND_DXGKDDIRECOMMENDFUNCTIONALVIDPN"></span>[*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)和[ *DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)  
-   如果显示微型端口驱动程序使用 DXGK\_\_ACPI 接收对[*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)函数的调用，则在*AcpiFlags*参数中设置\_显示\_模式标志，call center.dmm 将调用[*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)函数以获取新的 VidPN，并与当前的客户端 VidPN 进行比较。 如果两个 VidPNs 的拓扑是相同的，则 CALL CENTER.DMM 不会修改新的 VidPN。 否则，CALL CENTER.DMM 将从 VidPN 中删除模式信息，只保留拓扑，并使 CCD 数据库能够确定给定拓扑的模式。 然后，CALL CENTER.DMM 基于新的 VidPN 设置显示配置。

<span id="D3DKMTInvalidateActiveVidPn"></span><span id="d3dkmtinvalidateactivevidpn"></span><span id="D3DKMTINVALIDATEACTIVEVIDPN"></span>[**D3DKMTInvalidateActiveVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtinvalidateactivevidpn)  
-   在 Windows Vista 和更高版本中支持此功能，适用于版本 &lt; DXGKDDI\_INTERFACE\_版本\_WIN7 的显示微型端口驱动程序。 函数行为与 Windows Vista 上的行为相同。

-   此功能在 Windows 7 和更高版本中不受支持的显示器微型端口驱动程序版本 &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN7。 如果调用，则返回状态代码状态\_不\_支持。

 

 





