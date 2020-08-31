---
title: 设置 HDCP SRM 版本
description: 设置 HDCP SRM 版本
ms.assetid: 23f99f8f-7d13-4868-84fb-49245a81958b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c77cd4ab4eb17c4e0f0af600675523ea0b2ead33
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066630"
---
# <a name="setting-the-hdcp-srm-version"></a>设置 HDCP SRM 版本


OPM 配置可为受保护的输出设置内容保护 (HDCP) 系统 Renewability 消息 (SRM) 的版本。 若要设置版本，显示微型端口驱动程序的 [**DxgkDdiOPMConfigureProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output) 函数接收指向 [**DXGKMDT \_ OPM \_ 配置 \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters) 结构的指针，并将 **guidSetting** 成员设置为 DXGKMDT OPM \_ \_ set \_ hdcp \_ srm GUID，并将 **abParameters** 成员设置为指向 [**DXGKMDT \_ OPM \_ 集 \_ hdcp \_ srm \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_hdcp_srm_parameters) 结构的指针。 DXGKMDT \_ OPM \_ 集 \_ HDCP \_ SRM \_ 参数结构包含指定版本号的 ULONG。 最小有效位 (位0到 15) 包含以小字节序格式表示的 SRM 版本号。 有关 SRM 版本号的详细信息，请参阅 [HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

 

