---
title: 检测超量运行和欠量运行
description: 检测超量运行和欠量运行
ms.assetid: d7d282c8-adde-49fc-a20e-d633abd6dd3f
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14eed792f1d8c57a75d125d84fbffb4e2ddd025d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346332"
---
# <a name="detecting-overruns-and-underruns"></a>检测超量运行和欠量运行


## <span id="ddk_detecting_overruns_and_underruns_dtools"></span><span id="DDK_DETECTING_OVERRUNS_AND_UNDERRUNS_DTOOLS"></span>


可以使用**验证开始**或**验证结束**GFlags 中的选项可将从特殊池分配对齐，以便这些最佳适合检测溢出 （访问超过分配的内存） 或（访问位于开头分配的内存） 不足。

-   **验证开始**启用不足上从特殊池分配的检测。 当程序尝试访问上述特殊池内存分配的内存时，这会导致的 bug 检查。

-   **验证结束**启用从特殊池上分配溢出检测。 当程序尝试访问局限于其特殊池内存分配内存时，这会导致的 bug 检查。 因为溢出是更常见**验证结束**是默认值。

在 Windows Vista 和更高版本的 Windows 中，此选项才可用上**系统注册表**并**内核标志**选项卡。 在早期版本的 Windows，它是仅适用于**系统注册表**选项卡。

**若要指定特殊池对齐方式**

1.  单击**系统注册表**选项卡。

2.  单击**验证开始**或**验证结束**。

3.  单击 **“应用”**。

    下面的屏幕截图显示在系统上的验证开始和结束验证设置**注册表**选项卡。

    ![屏幕截图说明如何验证启动并验证在系统注册表选项卡上的最终选项](images/gflags-overruns.png)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**验证开始**并**验证结束**对齐方式设置适用于所有分配已从特殊的池，包括在驱动程序验证程序中设置的特殊池分配请求。 如果无需指定池标记或分配大小设置对齐方式，然后设置仅适用于在驱动程序验证程序中设置的请求。

 

 





