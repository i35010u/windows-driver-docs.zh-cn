---
title: OPM 和显示模式
description: OPM 和显示模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 837644799a099f05135af733aa3a8d63a6d060ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838489"
---
# <a name="opm-and-display-modes"></a>OPM 和显示模式


无论当前正在使用哪种显示模式，显示微型端口驱动程序都应报告与受保护的输出关联的物理连接器支持的所有保护类型。 当显示微型端口驱动程序使用 DXGKMDT OPM 接收对其 [**DxgkDdiOPMGetInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)或 [**DxgkDdiOPMGetCOPPCompatibleInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)函数的调用时，将会报告支持的保护类型 \_ 。 \_ 获取 \_ \_ \_ [**guidInformation \_ DXGKMDT \_ 获取 \_ 信息 \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_get_info_parameters)结构中设置 **的** 受支持保护类型。 有关检索受支持的保护类型的详细信息，请参阅检索有关受 [保护的输出的信息](retrieving-information-about-a-protected-output.md) 或 [检索有关受保护的输出的 COPP-Compatible 信息](retrieving-copp-compatible-information-about-a-protected-output.md)。

如果对于特定保护类型，当前解决方法太高，则当调用显示微型端口驱动程序的 [**DxgkDdiOPMConfigureProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output) 函数来为该保护类型设置保护级别时，驱动程序将返回错误。 以下方案举例说明了驱动程序的 *DxgkDdiOPMConfigureProtectedOutput* 函数应何时返回 success 以及何时出现错误：

-   如果受保护的输出与 S-视频输出连接器相关联，则对显示微型端口驱动程序的 *DxgkDdiOPMGetCOPPCompatibleInformation* 函数的调用 \_ 将使用 DXGKMDT OPM \_ 获取 \_ 受支持的 \_ 保护 \_ 类型。) 键入 (DXGKMDT \_ OPM \_ 保护 \_ 类型 \_ ACP) 支持模拟内容保护 (。 此后，如果调用驱动程序的 *DxgkDdiOPMConfigureProtectedOutput* 函数来为此连接器上的 ACP 类型设置级别，则驱动程序应返回成功，因为 s-视频的输出分辨率是固定的，即使桌面分辨率 (显示模式) 可能更高。

-   如果受保护的输出与组件输出连接器相关联，则对显示微型端口驱动程序的 *DxgkDdiOPMGetCOPPCompatibleInformation* 函数的调用 DXGKMDT \_ OPM \_ 获取支持的 \_ \_ 保护 \_ 类型也应指示 ACP 类型的支持。 但是，如果在显示分辨率为720p 或1080i 时调用驱动程序的 *DxgkDdiOPMConfigureProtectedOutput* 函数来为此输出设置 ACP 类型的级别，则驱动程序应返回状态 \_ 图形 \_ OPM \_ 分辨率 \_ 太 \_ 高的错误代码。 720p 或1080i 的分辨率太高，无法将 ACP 类型的保护级别设置为 on 组件输出连接器。

 

