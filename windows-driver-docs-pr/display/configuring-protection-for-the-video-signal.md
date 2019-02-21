---
title: 配置保护的视频信号
description: 配置保护的视频信号
ms.assetid: 557fc95b-1cf5-4b6d-b256-fe2db29ec0fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 515087445e362a99f87c3e953d060d5a5ad1f53c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521191"
---
# <a name="configuring-protection-for-the-video-signal"></a>配置保护的视频信号


OPM 配置可以配置为与受保护的输出相关联的物理连接器将经历的视频信号的保护。 若要设置信号保护，显示微型端口驱动程序[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)函数接收指向[ **DXGKMDT\_OPM\_配置\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560849)结构**guidSetting**成员设置为 DXGKMDT\_OPM\_集\_ACP\_AND\_CGMSA\_信号 GUID 并**abParameters**成员设置为一个指向[ **DXGKMDT\_OPM\_设置\_ACP\_AND\_CGMSA\_信号发送\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560913)结构，它指定如何保护信号。

 

 





