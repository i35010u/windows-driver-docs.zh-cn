---
title: 为视频信号配置保护
description: 为视频信号配置保护
ms.assetid: 557fc95b-1cf5-4b6d-b256-fe2db29ec0fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c86c7f7eee0adbd833fa30384e7e01516b723ecc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382353"
---
# <a name="configuring-protection-for-the-video-signal"></a>为视频信号配置保护


OPM 配置可以配置为与受保护的输出相关联的物理连接器将经历的视频信号的保护。 若要设置信号保护，显示微型端口驱动程序[ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数接收指向[ **DXGKMDT\_OPM\_配置\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)结构**guidSetting**成员设置为 DXGKMDT\_OPM\_集\_ACP\_AND\_CGMSA\_信号 GUID 并**abParameters**成员设置为一个指向[ **DXGKMDT\_OPM\_设置\_ACP\_AND\_CGMSA\_信号发送\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_acp_and_cgmsa_signaling_parameters)结构，它指定如何保护信号。

 

 





