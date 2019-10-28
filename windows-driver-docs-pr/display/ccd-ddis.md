---
title: CCD DDI
description: CCD DDI
ms.assetid: dde0e0b0-d6d0-4ca7-ae7e-427a650c080f
keywords:
- 微型端口驱动程序 WDK 显示，连接和配置显示（CCD）
- 连接和配置显示（CCD） WDK 显示
- CCD （连接和配置显示） WDK 显示
ms.date: 10/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 03ab7e2702ffec0f4e556f5e1ae0ad4a570b137b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839816"
---
# <a name="ccd-ddis"></a>CCD DDI


Windows 7 中引入的连接和配置显示（CCD）功能提供了改进的显示设备的显示微型端口驱动程序控制。 

## <a name="ccd-ddis-for-display-miniport-drivers"></a>用于显示微型端口驱动程序的 CCD DDIs

以下参考主题介绍了可用于显示微型端口驱动程序的开发人员的 CCD 设备驱动程序接口（DDIs）：

<span id="System-Implemented_Functions"></span><span id="system-implemented_functions"></span><span id="SYSTEM-IMPLEMENTED_FUNCTIONS"></span>**系统实现的函数**  

|||
|:--|:--|
|[**DXGK\_监视器\_接口\_V2：:p fnGetAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_getadditionalmonitormodeset)|[**DXGK\_监视器\_接口\_V2：:p fnReleaseAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_releaseadditionalmonitormodeset)|

<span id="Driver-Implemented_Function"></span><span id="driver-implemented_function"></span><span id="DRIVER-IMPLEMENTED_FUNCTION"></span>**驱动程序实现的函数**

以下函数必须通过支持 CCD 的显示微型端口驱动程序来实现：

[**DxgkDdiQueryVidPnHWCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)

<span id="Structures"></span><span id="structures"></span><span id="STRUCTURES"></span>**构造**

|||
|:--|:--|
|[**D3DKMDT\_VIDPN\_HW\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)|[**D3DKMDT\_VIDPN\_提供\_路径\_缩放\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)|
|[**D3DKMT\_POLLDISPLAYCHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_polldisplaychildren)|[**D3DKMT\_RENDERFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_renderflags)|
|[**DISPLAYID\_详细\_计时\_类型\_I\_纵横比**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_aspect_ratio)|[**DXGKARG\_QUERYVIDPNHWCAPABILITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryvidpnhwcapability)|
|[**DXGK\_监视器\_接口\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface_v2)|[**DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)|
|[**DXGK\_TARGETMODE\_详细\_计时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_targetmode_detail_timing)||

<span id="Enumerations"></span><span id="enumerations"></span><span id="ENUMERATIONS"></span>**计数**

|||
|:--|:--|
|[**D3DKMDT\_VIDPN\_提供\_路径\_缩放**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling)|[**DISPLAYID\_详细\_计时\_类型\_I\_纵横比**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_aspect_ratio)|
|[**DISPLAYID\_详细\_计时\_类型\_I\_扫描\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_scanning_mode)|[**DISPLAYID\_详细\_计时\_类型\_I\_立体声\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_stereo_mode)|
|[**DISPLAYID\_详细\_计时\_类型\_我\_同步\_极性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_sync_polarity)||


有关如何在显示微型端口驱动程序中实现 CCD 的更多详细信息，请参阅以下主题：

[获取更多监视目标模式](obtaining-additional-monitor-target-modes.md)

[使用纵横比和自定义缩放模式](using-aspect-ratio-and-custom-scaling-modes.md)

[建议 VidPN 拓扑的系统调用](system-calls-to-recommend-vidpn-topology.md)

[ACPI 键盘快捷方式逻辑](acpi-keyboard-shortcut-logic.md)

[查询 VidPN 硬件功能](querying-vidpnhardware-capabilities.md)


