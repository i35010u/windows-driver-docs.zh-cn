---
title: 设置受保护输出的保护级别
description: 设置受保护输出的保护级别
ms.assetid: 2f041190-8001-4e79-8398-8b642884f751
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4b50189dce5f913e75fa8cdd9cbe6c26472cbbb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829499"
---
# <a name="setting-the-protection-level-for-a-protected-output"></a>设置受保护输出的保护级别


OPM 配置可以在受保护的输出上设置保护类型的保护级别。 若要设置保护级别，显示微型端口驱动程序的[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数接收指向[**DXGKMDT\_OPM 的指针\_使用 GUIDSETTING 配置\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)结构将成员设置为 DXGKMDT\_OPM\_将\_保护\_级别 GUID 和**abParameters**成员设置为指向[**DXGKMDT\_OPM\_\_\_\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_protection_level_parameters)结构，指定要设置的保护类型以及设置保护的级别。 对于指定的保护类型，可以设置以下保护级别：

-   对于 DXGKMDT\_OPM\_保护\_在 DXGKMDT\_OPM 的**ulProtectionType**成员中指定\_ACP\_设置\_保护\_级别\_参数[**DXGKMDT\_OPM\_\_\_ACP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level)中的值可以在 DXGKMDT\_OPM\_设置\_保护的**ulProtectionLevel**成员中指定\_级别\_参数。

-   对于 DXGKMDT\_OPM\_保护\_在 DXGKMDT\_OPM 的**ulProtectionType**成员中指定\_CGMSA\_设置\_保护\_级别\_参数可以在 DXGKMDT\_OPM 的**ulProtectionLevel**成员中指定[**DXGKMDT\_OPM\_CGMSA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)枚举中的值\_设置\_保护\_级别\_参数。

-   对于 DXGKMDT\_OPM\_保护\_类型\_HDCP 或 DXGKMDT\_OPM **\_COPP\_** 类型\_\_\_\_OPM\_设置\_保护\_级别\_参数，DXGKMDT 中的某个保护级别值\_\_\_[**LEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)枚举可在DXGKMDT\_OPM 的**ulProtectionLevel**成员\_\_保护\_级别\_参数设置。

-   对于 DXGKMDT\_OPM\_保护\_在 DXGKMDT\_OPM 的**ulProtectionType**成员中指定\_DPCP\_设置\_保护\_级别\_参数[**DXGKMDT\_OPM\_\_\_DPCP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_dpcp_protection_level)中的值可以在 DXGKMDT\_OPM\_设置\_保护的**ulProtectionLevel**成员中指定\_级别\_参数。

**请注意**   DXGKMDT\_OPM\_设置\_保护\_\_\_的\_\_DVD GUID 是适用于 Windows 7 的新手，并用于指示驱动程序应启用 HDCP根据新的 CSS 规则。 将 DXGKMDT\_OPM\_设置\_保护\_级别的\_\_\_CSS\_DVD 命令与设置现有 DXGKMDT\_OPM\_设置\_保护完全相同除了 DXGKMDT\_OPM\_设置\_保护\_级别\_\_LEVEL 命令以外，\_CSS\_DVD 没有绝对要求来启用请求的保护。

 

 

 





