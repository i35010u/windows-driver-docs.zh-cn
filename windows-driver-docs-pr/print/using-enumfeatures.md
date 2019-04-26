---
title: 使用 EnumFeatures
description: 使用 EnumFeatures
ms.assetid: 4a87cedf-066a-445b-ad3e-71699c9d3e07
keywords:
- EnumFeatures
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91e0ec6a79b5bd380a8a01cf6d0027bf5654adaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330309"
---
# <a name="using-enumfeatures"></a>使用 EnumFeatures





可以使用调用方**EnumFeatures**检索关键字列表，其中包含当前支持的驱动程序功能和 PPD 的所有功能，此外所示，就好像 PPD中定义的功能，将视为Pscript\*OpenUI /\*CloseUI 结构关键字：

\*LeadingEdge

\*UseHWMargins

Pscript 以特殊方式处理某些功能。 如果多个之一\*分辨率\*SetResolution，和\*JCLResolution 关键字出现在 PPD，它们合并到一个标准的功能。 合并后，该功能的关键字名称将是"JCLResolution"如果\*JCLResolution 显示第一个; 否则它将为"解决方法"。

**请注意**  某些驱动程序功能 (如 %镜像) 始终受支持，当仅在某些情况下支持的其他驱动程序功能时。 例如，当在 Windows 2000 和更高版本操作系统上禁用后台处理程序 EMF 后台处理时释放，%pageorder 不支持功能。 这些不受支持的驱动程序功能不会出现在输出关键字列表**EnumFeatures**。

 

有关驱动程序功能，在输出中包含关键字前缀"%"。 有关 PPD 功能，关键字前缀"\*"不包含在输出。

 

 




