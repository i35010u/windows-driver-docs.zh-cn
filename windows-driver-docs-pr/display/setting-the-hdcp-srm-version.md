---
title: 设置 HDCP SRM 版本
description: 设置 HDCP SRM 版本
ms.assetid: 23f99f8f-7d13-4868-84fb-49245a81958b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bef223ebad9ccb791cdac6f5b2b1b57610b972ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365545"
---
# <a name="setting-the-hdcp-srm-version"></a>设置 HDCP SRM 版本


OPM 配置可以设置版本的高带宽数字内容保护 (HDCP) 系统可更新性消息 (SRM) 为受保护的输出。 若要设置的版本中，显示微型端口驱动程序的[ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数接收指向[ **DXGKMDT\_OPM\_配置\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)结构**guidSetting**成员设置为 DXGKMDT\_OPM\_设置\_HDCP\_SRM GUID 和**abParameters**成员设置为一个指向[ **DXGKMDT\_OPM\_设置\_HDCP\_SRM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_hdcp_srm_parameters)结构。 DXGKMDT\_OPM\_设置\_HDCP\_SRM\_参数结构包含的 ULONG 的指定的版本号。 最低有效位 （位 0 到 15） 包含在 little-endian 格式 SRM 的版本号。 有关 SRM 版本号的详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

 

 





