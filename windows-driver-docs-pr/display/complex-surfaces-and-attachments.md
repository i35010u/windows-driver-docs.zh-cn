---
title: 复杂图面和附件
description: 复杂图面和附件
ms.assetid: fb75c534-b1ff-44d3-a8dc-dcf0f221b6ad
keywords:
- 绘图图面相 WDK DirectDraw，复杂
- DirectDraw 图面 WDK Windows 2000 显示复杂
- WDK DirectDraw，复杂的图面
- 复杂的图面 WDK DirectDraw
- WDK DirectDraw，附件的图面
- 绘图图面相 WDK DirectDraw，附件
- DirectDraw 面，WDK Windows 2000 显示，附件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04f6fe1cf0643d10488e9bf23a7504b8751f4187
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342443"
---
# <a name="complex-surfaces-and-attachments"></a>复杂图面和附件


## <span id="ddk_complex_surfaces_and_attachments_gg"></span><span id="DDK_COMPLEX_SURFACES_AND_ATTACHMENTS_GG"></span>


可以是图面*复杂*，这意味着它们是较大的应用层协议关联集合的一部分。 复杂的应用层的示例包括前台缓冲区和相关联的后台缓冲区，各种级别的 MIP 映射，以及各种人脸的多维数据集映射。

DirectDraw 运行时使用名为的概念*图面附件*管理链接的不同简单到复杂的曲面的图面。 图面可以隐式地为应用程序时发出一个调用附加**IDirectDraw7::CreateSurface**生成翻转链 （前台缓冲区和后台缓冲区有一个可能的 Z 缓冲）; 或显式作为时应用程序将 Z 缓冲区与呈现目标相关联通过调用**IDirectDrawSurface7::AddAttachedSurface**。

 

 





