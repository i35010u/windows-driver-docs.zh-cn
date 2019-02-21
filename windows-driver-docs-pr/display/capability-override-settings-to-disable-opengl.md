---
title: 功能重写的设置为禁用 OpenGL
description: 所有的框中显示 Inf 此软件设备设置可确保没有现成的驱动程序将面临开箱 OpenGL ICDs 的互操作性问题。
ms.assetid: 70903938-4A89-45A3-B1AD-B823C5735AB1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0d694a29aec1b1da8536772bf78d73b14e3a66d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547702"
---
# <a name="capability-override-settings-to-disable-opengl"></a>功能重写的设置为禁用 OpenGL


所有的框中显示 Inf 此软件设备设置可确保没有现成的驱动程序将面临开箱 OpenGL ICDs 的互操作性问题。

例如：

``` syntax
[R200_SoftwareDeviceSettings]
HKR,, CapabilityOverride,                       %REG_DWORD%,    0x8
```

 

 





