---
title: 设置 HDCP SRM 版本
description: 设置 HDCP SRM 版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd64e1a01f2d0ce0243a3e9e828694f551a75fae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828033"
---
# <a name="setting-the-hdcp-srm-version"></a>设置 HDCP SRM 版本


OPM 配置可为受保护的输出设置内容保护 (HDCP) 系统 Renewability 消息 (SRM) 的版本。 若要设置版本，显示微型端口驱动程序的 [**DxgkDdiOPMConfigureProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output) 函数接收指向 [**DXGKMDT \_ OPM \_ 配置 \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters) 结构的指针，并将 **guidSetting** 成员设置为 DXGKMDT OPM \_ \_ set \_ hdcp \_ srm GUID，并将 **abParameters** 成员设置为指向 [**DXGKMDT \_ OPM \_ 集 \_ hdcp \_ srm \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_hdcp_srm_parameters) 结构的指针。 DXGKMDT \_ OPM \_ 集 \_ HDCP \_ SRM \_ 参数结构包含指定版本号的 ULONG。 最小有效位 (位0到 15) 包含以小字节序格式表示的 SRM 版本号。 有关 SRM 版本号的详细信息，请参阅 [HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

 

