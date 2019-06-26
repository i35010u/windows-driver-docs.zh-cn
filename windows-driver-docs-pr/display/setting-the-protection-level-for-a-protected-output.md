---
title: 设置受保护输出的保护级别
description: 设置受保护输出的保护级别
ms.assetid: 2f041190-8001-4e79-8398-8b642884f751
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a218a007d0fbf7599b294555b779d6d8f1568852
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365543"
---
# <a name="setting-the-protection-level-for-a-protected-output"></a>设置受保护输出的保护级别


OPM 配置可以在受保护的输出设置保护类型的保护级别。 若要设置的保护级别，显示微型端口驱动程序的[ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数接收指向[ **DXGKMDT\_OPM\_配置\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)结构**guidSetting**成员设置为 DXGKMDT\_OPM\_集\_保护\_级别 GUID 和**abParameters**成员设置为一个指向[ **DXGKMDT\_OPM\_设置\_保护\_级别\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_protection_level_parameters)结构，它指定到保护组和要设置的保护级别的类型。 可以为所指示的保护类型设置以下保护级别：

-   有关 DXGKMDT\_OPM\_PROTECTION\_类型\_中指定的 ACP **ulProtectionType** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数中的保护级别值之一[ **DXGKMDT\_OPM\_ACP\_保护\_级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level)枚举中只能指定**ulProtectionLevel** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数。

-   有关 DXGKMDT\_OPM\_保护\_类型\_中指定 CGMSA **ulProtectionType** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数中的保护级别值之一[ **DXGKMDT\_OPM\_CGMSA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)枚举可以在中指定**ulProtectionLevel** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数。

-   有关 DXGKMDT\_OPM\_PROTECTION\_类型\_HDCP 或 DXGKMDT\_OPM\_保护\_类型\_COPP\_兼容\_中指定 HDCP **ulProtectionType** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_之一的参数保护级别值从[ **DXGKMDT\_OPM\_HDCP\_保护\_级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)中只能指定枚举**ulProtectionLevel** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数。

-   有关 DXGKMDT\_OPM\_保护\_类型\_中指定 DPCP **ulProtectionType** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数中的保护级别值之一[ **DXGKMDT\_OPM\_DPCP\_保护\_级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgkmdt_dpcp_protection_level)枚举中只能指定**ulProtectionLevel** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数。

**请注意**   DXGKMDT\_OPM\_设置\_保护\_级别\_ACCORDING\_TO\_CSS\_DVD GUID 是新增功能Windows 7 和用来指示驱动程序应根据新的 CSS 规则启用 HDCP。 设置 DXGKMDT\_OPM\_设置\_保护\_级别\_ACCORDING\_TO\_CSS\_DVD 命令等同于设置现有 DXGKMDT\_OPM\_设置\_保护\_除该 DXGKMDT 级别命令\_OPM\_设置\_保护\_级别\_根据\_TO\_CSS\_DVD 具有绝对无需启用请求的保护。

 

 

 





