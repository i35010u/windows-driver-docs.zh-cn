---
title: 禁用 OpenGL 互操作性
description: 禁用 OpenGL 互操作性
keywords:
- INF 文件，WDK 显示，互操作性
- 互操作性 WDK 显示
- OpenGL WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1835c616d943df5233de531a5c74784334e328d5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809287"
---
# <a name="disabling-interoperability-with-opengl"></a>禁用 OpenGL 互操作性


若要确保不会向具有 OpenGL 可安装客户端驱动程序的互操作性问题公开 Microsoft Direct3D 显示驱动程序 (ICDs) ，必须在 INF 的 "添加注册表" 部分中设置以下项：

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, CapabilityOverride,    %REG_DWORD%, 0x8
```

 

 





