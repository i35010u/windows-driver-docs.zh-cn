---
title: 设置 HDCP SRM 版本
description: 设置 HDCP SRM 版本
ms.assetid: 23f99f8f-7d13-4868-84fb-49245a81958b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 193c8db216f7a02a907c4e1b91971e39d926b942
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390434"
---
# <a name="setting-the-hdcp-srm-version"></a>设置 HDCP SRM 版本


OPM 配置可以设置版本的高带宽数字内容保护 (HDCP) 系统可更新性消息 (SRM) 为受保护的输出。 若要设置的版本中，显示微型端口驱动程序的[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)函数接收指向[ **DXGKMDT\_OPM\_配置\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560849)结构**guidSetting**成员设置为 DXGKMDT\_OPM\_设置\_HDCP\_SRM GUID 和**abParameters**成员设置为一个指向[ **DXGKMDT\_OPM\_设置\_HDCP\_SRM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560915)结构。 DXGKMDT\_OPM\_设置\_HDCP\_SRM\_参数结构包含的 ULONG 的指定的版本号。 最低有效位 （位 0 到 15） 包含在 little-endian 格式 SRM 的版本号。 有关 SRM 版本号的详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

 

 





