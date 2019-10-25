---
title: 设置 HDCP SRM 版本
description: 设置 HDCP SRM 版本
ms.assetid: 23f99f8f-7d13-4868-84fb-49245a81958b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99169cffde19a73b054a300fed8566be6289f0e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829497"
---
# <a name="setting-the-hdcp-srm-version"></a>设置 HDCP SRM 版本


OPM 配置可为受保护的输出设置高带宽数字内容保护（HDCP）系统 Renewability 消息（SRM）的版本。 若要设置版本，则显示微型端口驱动程序的[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数接收指向[**DXGKMDT\_OPM 的指针\_配置\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)结构，并将**guidSetting**成员设置为DXGKMDT\_OPM\_将\_HDCP\_SRM GUID 和**abParameters**成员设置为指向[**DXGKMDT\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_hdcp_srm_parameters)\_\_\_HDCP\_ DXGKMDT\_OPM\_集\_HDCP\_SRM\_参数结构包含指定版本号的 ULONG。 最小有效位（位0到15）包含 SRM 的版本编号（以小字节序格式）。 有关 SRM 版本号的详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

 

 





