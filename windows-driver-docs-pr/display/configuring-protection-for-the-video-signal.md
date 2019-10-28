---
title: 为视频信号配置保护
description: 为视频信号配置保护
ms.assetid: 557fc95b-1cf5-4b6d-b256-fe2db29ec0fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2775ba5c7876497edb6c5859c2b456b0ba63da2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839794"
---
# <a name="configuring-protection-for-the-video-signal"></a>为视频信号配置保护


OPM 配置可以为通过与受保护的输出关联的物理连接器的视频信号配置保护。 若要设置信号保护，显示微型端口驱动程序的[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数接收指向 DXGKMDT\_OPM 的指针\_使用**guidSetting**成员[**配置\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)结构设置为 DXGKMDT\_OPM\_设置\_ACP\_，\_CGMSA\_信号 GUID 和**abParameters**成员设置为指向[**DXGKMDT\_OPM\_\_\_ACP和\_CGMSA\_通知\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_acp_and_cgmsa_signaling_parameters)指定如何保护信号的参数结构。

 

 





