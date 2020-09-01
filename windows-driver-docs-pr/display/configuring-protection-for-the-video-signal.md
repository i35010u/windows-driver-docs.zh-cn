---
title: 为视频信号配置保护
description: 为视频信号配置保护
ms.assetid: 557fc95b-1cf5-4b6d-b256-fe2db29ec0fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 111238e426219a936a9aeb35ae86f5959bf1ff91
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064898"
---
# <a name="configuring-protection-for-the-video-signal"></a>为视频信号配置保护


OPM 配置可以为通过与受保护的输出关联的物理连接器的视频信号配置保护。 若要设置信号保护，显示微型端口驱动程序的 [**DxgkDdiOPMConfigureProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output) 函数接收指向 [**DXGKMDT \_ OPM \_ 配置 \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters) 结构的指针，并将 **guidSetting** 成员设置为 DXGKMDT \_ OPM \_ set \_ ACP 和 CGMSA \_ \_ \_ 信号 GUID，并将 **abParameters** 成员设置为指向 [**DXGKMDT \_ OPM \_ set \_ ACP \_ 和 CGMSA 信号 \_ \_ \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_acp_and_cgmsa_signaling_parameters) 结构的指针，该结构指定如何保护信号。

 

