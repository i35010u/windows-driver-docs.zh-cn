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


OPM 配置可以在受保护的输出上设置保护类型的保护级别。 若要设置保护级别，则显示微型端口驱动程序的[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数接收指向[**DXGKMDT\_OPM 的指针\_配置\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)结构，并将**guidSetting**成员设置为 DXGKMDT\_OPM\_设置\_保护\_级别 GUID，并将**ABPARAMETERS**成员设置为指向[**DXGKMDT\_OPM\_\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_protection_level_parameters)结构，它指定要设置的保护类型以及设置保护的级别。 对于指定的保护类型，可以设置以下保护级别：

-   对于 DXGKMDT\_OPM\_保护\_类型为 DXGKMDT\_OPM 的**ulProtectionType**成员中指定的\_ACP\_设置\_保护\_级别\_参数， [**DXGKMDT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level)\_OPM\_ACP\_level 枚举中的一个保护级别值可**在 ulProtectionLevel\_** DXGKMDT\_\_\_\_\_参数。

-   对于 DXGKMDT\_OPM\_保护\_在 DXGKMDT\_OPM 的**ulProtectionType**成员中指定\_CGMSA\_设置\_保护\_级别\_参数，可以在 DXGKMDT\_OPM\_\_\_\_\_\_参数的**CGMSA**成员中指定 ULPROTECTIONLEVEL DXGKMDT [**OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)枚举中的某个保护级别值。

-   对于 DXGKMDT\_OPM\_保护\_类型\_HDCP 或 DXGKMDT\_OPM\_保护\_类型\_COPP\_**ulProtectionType 成员中指定 DXGKMDT\_** OPM\_设置\_保护\_级别\_参数，可在中指定[**DXGKMDT\_OPM\_hdcp\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)枚举中的其中一个保护级别的值DXGKMDT\_OPM 的**ulProtectionLevel**成员\_\_保护\_级别\_参数设置。\_\_

-   对于 DXGKMDT\_OPM\_保护\_在 DXGKMDT\_OPM 的**ulProtectionType**成员中指定\_DPCP\_设置\_保护\_等级\_参数， [**DXGKMDT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_dpcp_protection_level)\_OPM\_DPCP\_level 枚举中的某个保护级别值可**在 ulProtectionLevel\_** DXGKMDT\_\_\_\_\_参数。

**请注意**   "DXGKMDT\_OPM\_设置\_保护\_"\_"\_"\_"\_" "" "" " 将 DXGKMDT\_OPM\_将\_CSS\_DVD 命令设置为\_CSS\_DVD 命令\_保护\_级别设置与设置现有 DXGKMDT\_OPM\_设置\_保护\_LEVEL 命令相同，不同之处在于，DXGKMDT\_OPM\_\_\_\_\_\_\_

 

 

 





