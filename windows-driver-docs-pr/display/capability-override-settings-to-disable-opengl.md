---
title: 用于禁用 OpenGL 的功能覆盖设置
description: 对于所有内置的显示 Inf，此软件设备设置可确保无机箱内驱动程序会暴露给内置 OpenGL ICDs 可能的互操作性问题。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06cc9786deb2f4e17e1d6e4dab375837516a6c1b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810375"
---
# <a name="capability-override-settings-to-disable-opengl"></a>用于禁用 OpenGL 的功能覆盖设置


对于所有内置的显示 Inf，此软件设备设置可确保无机箱内驱动程序会暴露给内置 OpenGL ICDs 可能的互操作性问题。

例如：

``` syntax
[R200_SoftwareDeviceSettings]
HKR,, CapabilityOverride,                       %REG_DWORD%,    0x8
```

 

 





