---
title: FVF（灵活顶点格式）
description: FVF（灵活顶点格式）
ms.assetid: 206f4275-bcb8-4e8e-9c11-c6fb5d9c561d
keywords:
- 顶点格式 WDK Direct3D
- 灵活的顶点格式 WDK Direct3D
- FVF WDK Direct3D
- Direct3D WDK Windows 2000 显示，灵活顶点格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c94d4dda73a0bbb950ac4ce96257c4595fbc575
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377991"
---
# <a name="fvf-flexible-vertex-format"></a>FVF（灵活顶点格式）


## <span id="ddk_fvf_gg"></span><span id="DDK_FVF_GG"></span>


在驱动程序[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)回调接收灵活顶点格式 (FVF) 中的顶点数据。 顶点格式非常灵活，因为没有为该数据定义任何全面的数据结构。 驱动程序必须实现完整 FVF 功能。

没有 FVF 更新 Microsoft DirectX 7.0 包括 1d，3D，和 4d 除了常用的 2D 纹理的纹理。 有关此更新的详细信息，请参阅[FVF 更新](fvf-update.md)。 请参阅*Perm3*示例驱动程序和 DirectX SDK 文档，了解有关这些主题的详细信息。

**请注意**   Microsoft Windows Driver Kit (WDK) 不包含 3Dlabs Permedia3 示例显示器驱动程序 (*Perm3.h*)。 你可以获取从 Windows Server 2003 SP1 驱动程序开发工具包 (DDK)，可以从 DDK-WDHC 网站的 Windows 驱动程序开发工具包页面下载此示例驱动程序。

 

 

 





