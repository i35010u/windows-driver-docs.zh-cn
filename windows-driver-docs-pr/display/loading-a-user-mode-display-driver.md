---
title: 加载用户模式显示驱动程序
description: 加载用户模式显示驱动程序
keywords:
- INF 文件，WDK 显示，用户模式驱动程序加载
- 用户模式显示驱动程序 WDK Windows Vista，加载
- 正在加载驱动程序 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e0870d823302a8fa306fe4c73a904cdf8e9534e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792289"
---
# <a name="loading-a-user-mode-display-driver"></a>加载用户模式显示驱动程序


你必须在 INF 文件的 "外接程序" 部分中设置以下项，以便在安装驱动程序时将用户模式显示驱动程序的 DLL 名称添加到注册表中，以便 Microsoft Direct3D 运行时可以随后加载 DLL：

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDriverName,    %REG_MULTI_SZ%, Xxx.dll
```

INF 文件必须包含信息，以指示操作系统将用户模式显示驱动程序复制到系统的% systemroot% \\ system32 目录。 有关详细信息，请参阅 [**Inf CopyFiles 指令**](../install/inf-copyfiles-directive.md) 和 [**inf DestinationDirs 部分**](../install/inf-destinationdirs-section.md)。

Direct3D 运行时从注册表获取用户模式显示驱动程序的 DLL 名称，以便在运行时的进程空间中加载用户模式显示驱动程序。

 

