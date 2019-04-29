---
title: 用于禁用 OpenGL 的功能覆盖设置
description: 所有的框中显示 Inf 此软件设备设置可确保没有现成的驱动程序将面临开箱 OpenGL ICDs 的互操作性问题。
ms.assetid: 70903938-4A89-45A3-B1AD-B823C5735AB1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0d694a29aec1b1da8536772bf78d73b14e3a66d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385682"
---
# <a name="capability-override-settings-to-disable-opengl"></a>用于禁用 OpenGL 的功能覆盖设置


所有的框中显示 Inf 此软件设备设置可确保没有现成的驱动程序将面临开箱 OpenGL ICDs 的互操作性问题。

例如：

``` syntax
[R200_SoftwareDeviceSettings]
HKR,, CapabilityOverride,                       %REG_DWORD%,    0x8
```

 

 





