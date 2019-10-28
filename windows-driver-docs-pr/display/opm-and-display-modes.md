---
title: OPM 和显示模式
description: OPM 和显示模式
ms.assetid: d412a32b-7afd-4f48-9b8e-7cf66533349f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af790b4c698e9a8285d8b63d69d1612a79f16efe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840496"
---
# <a name="opm-and-display-modes"></a>OPM 和显示模式


无论当前正在使用哪种显示模式，显示微型端口驱动程序都应报告与受保护的输出关联的物理连接器支持的所有保护类型。 显示微型端口驱动程序在收到对其[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)或[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)函数的调用（DXGKMDT\_OPM\_GET\_支持）时报告支持的保护类型 @no在 DXGKMDT\_OPM 的**guidInformation**成员中设置的 __t_7_ 保护\_类型[ **\_获取\_信息\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_get_info_parameters)结构。 有关检索受支持的保护类型的详细信息，请参阅检索有关受[保护的输出的信息](retrieving-information-about-a-protected-output.md)或[检索有关受保护的输出的 COPP 兼容信息](retrieving-copp-compatible-information-about-a-protected-output.md)。

如果对于特定保护类型，当前解决方法太高，则当调用显示微型端口驱动程序的[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数来为该保护类型设置保护级别时，驱动程序将返回错误。 以下方案举例说明了驱动程序的*DxgkDdiOPMConfigureProtectedOutput*函数应何时返回 success 以及何时出现错误：

-   如果受保护的输出与 S-视频输出连接器相关联，则对显示微型端口驱动程序的*DxgkDdiOPMGetCOPPCompatibleInformation*函数的调用 DXGKMDT\_OPM\_获取\_支持\_保护\_类型集应指示支持模拟内容保护（ACP）类型（DXGKMDT\_OPM\_保护\_类型\_ACP）。 此后，如果调用驱动程序的*DxgkDdiOPMConfigureProtectedOutput*函数来为此连接器上的 ACP 类型设置级别，则驱动程序应返回 success，因为 s-视频的输出分辨率是固定的，即使桌面分辨率（显示模式）可能会更高。

-   如果受保护的输出与组件输出连接器相关联，则对显示微型端口驱动程序的*DxgkDdiOPMGetCOPPCompatibleInformation*函数的调用 DXGKMDT\_OPM\_获取\_支持\_保护\_类型还应指示对 ACP 类型的支持。 但是，如果在显示分辨率为720p 或1080i 时调用驱动程序的*DxgkDdiOPMConfigureProtectedOutput*函数来为此输出设置 ACP 类型的级别，则驱动程序应\_OPM 返回状态\_图形\_解决方法\_太\_高错误代码。 720p 或1080i 的分辨率太高，无法将 ACP 类型的保护级别设置为 on 组件输出连接器。

 

 





