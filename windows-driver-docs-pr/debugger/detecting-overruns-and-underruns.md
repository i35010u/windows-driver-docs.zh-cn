---
title: 检测超量运行和欠量运行
description: 检测超量运行和欠量运行
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c99f7e036b6010dae0cce814dbcbb3f5449f572
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794029"
---
# <a name="detecting-overruns-and-underruns"></a>检测超量运行和欠量运行


## <span id="ddk_detecting_overruns_and_underruns_dtools"></span><span id="DDK_DETECTING_OVERRUNS_AND_UNDERRUNS_DTOOLS"></span>


您可以使用 GFlags 中的 " **验证启动** " 或 " **验证结束** " 选项来对齐特定池的分配，以便它们最适用于检测 (访问超过分配末尾的内存) 或不足 (访问分配) 开头之前的内存。

-   **验证 "开始** " 将对来自特殊池的分配启用不足检测。 这会在程序尝试在其特殊池内存分配之前访问内存时导致 bug 检查。

-   **验证最终** 对来自特殊池的分配启用超限检测。 当程序尝试访问超出其特殊池内存分配的内存时，这会导致 bug 检查。 由于溢出更常见，因此 **验证 End** 是默认值。

在 Windows Vista 和更高版本的 Windows 中，可以在 " **系统注册表** " 和 " **内核标志** " 选项卡上使用此选项。 在 Windows 的早期版本中，它仅在 " **系统注册表** " 选项卡上可用。

**指定特殊的池对齐方式**

1.  单击 " **系统注册表** " 选项卡。

2.  单击 "验证" " **开始** " 或 " **验证结束**"。

3.  单击“应用” 。

    以下屏幕截图显示了 "系统 **注册表** " 选项卡上的 "验证启动并验证结束" 设置。

    ![说明 "系统注册表" 选项卡上的 "验证启动并验证结束" 选项的屏幕截图](images/gflags-overruns.png)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**验证 "开始**" 和 "**验证结束**" 对齐设置适用于特殊池的所有分配，包括在驱动程序验证程序中设置的特殊池分配请求。 如果在未指定池标记或分配大小的情况下设置对齐方式，则这些设置仅适用于在驱动程序验证程序中设置的请求。

 

 





