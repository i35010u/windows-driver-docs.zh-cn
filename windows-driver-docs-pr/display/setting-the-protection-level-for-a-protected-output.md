---
title: 设置受保护输出的保护级别
description: 设置受保护输出的保护级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d114aba6d7c3ad6ef114d065d7f81ca82bdc8b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822465"
---
# <a name="setting-the-protection-level-for-a-protected-output"></a>设置受保护输出的保护级别


OPM 配置可以在受保护的输出上设置保护类型的保护级别。 若要设置保护级别，则显示微型端口驱动程序的 [**DxgkDdiOPMConfigureProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output) 函数接收指向 [**DXGKMDT \_ OPM \_ 配置 \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters) 结构的指针，并将 **guidSetting** 成员设置为 DXGKMDT OPM \_ \_ set \_ 保护 \_ 级别 GUID，并将 **abParameters** 成员设置为指向 [**DXGKMDT \_ OPM \_ set \_ protection \_ level \_ PARAMETERS**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_protection_level_parameters) 结构的指针，该结构指定要设置的保护类型以及设置保护的级别。 对于指定的保护类型，可以设置以下保护级别：

-   对于 \_ DXGKMDT OPM \_ \_ \_ Set protection level 参数 **ULPROTECTIONTYPE** 成员中指定的 DXGKMDT OPM PROTECTION TYPE ACP \_ \_ \_ \_ \_ ，可以在 DXGKMDT OPM **ulProtectionLevel** set protection level 参数的 ACP 成员中指定 [**ulProtectionLevel DXGKMDT OPM \_ \_ \_ 保护 \_ 级别**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level)枚举中的一个保护级别值 \_ \_ \_ \_ \_ 。

-   对于 \_ DXGKMDT OPM \_ \_ \_ Set protection level 参数 **ULPROTECTIONTYPE** 成员中指定的 DXGKMDT OPM PROTECTION TYPE CGMSA \_ \_ \_ \_ \_ ，可以在 DXGKMDT OPM **ulProtectionLevel** set protection level 参数的 CGMSA 成员中指定 [**ulProtectionLevel \_ DXGKMDT \_ OPM**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)枚举中的某个保护级别值 \_ \_ \_ \_ \_ 。

-   对于 COPP ulProtectionType set protection level \_ 参数的 DXGKMDT 成员中指定的 DXGKMDT OPM \_ protection \_ 类型 \_ hdcp 或 DXGKMDT \_ OPM \_ 保护 \_ 类型 \_ OPM 兼容的 \_ \_ **ulProtectionType** hdcp \_ \_ \_ \_ \_ ，可以在 DXGKMDT OPM 设置保护级别参数的 **ulProtectionLevel** 成员中指定 [**DXGKMDT \_ OPM \_ HDCP \_ 保护 \_**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)级别枚举中的某个保护级别值 \_ \_ \_ \_ \_ 。

-   对于 \_ DXGKMDT OPM \_ \_ \_ Set protection level 参数 **ULPROTECTIONTYPE** 成员中指定的 DXGKMDT OPM PROTECTION TYPE DPCP \_ \_ \_ \_ \_ ，可以在 DXGKMDT OPM **ulProtectionLevel** set protection level 参数的 DPCP 成员中指定 [**ulProtectionLevel DXGKMDT OPM \_ \_ \_ 保护 \_ 级别**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_dpcp_protection_level)枚举中的一个保护级别值 \_ \_ \_ \_ \_ 。

**注意**   DXGKMDT \_ OPM \_ \_ \_ \_ 根据 \_ css DVD GUID 设置保护 \_ 级别 \_ 是适用于 Windows 7 的新功能，用于指示驱动程序应根据新 CSS 规则启用 HDCP。 设置 DXGKMDT \_ OPM \_ \_ \_ \_ 根据 css dvd 命令设置保护级别与 \_ \_ \_ 设置现有 DXGKMDT \_ OPM \_ set \_ protection level 命令相同， \_ 不同之处在于： DXGKMDT \_ OPM \_ \_ \_ 根据 CSS dvd 设置保护级别 \_ \_ \_ \_ 没有启用所请求保护的绝对要求。

 

 

