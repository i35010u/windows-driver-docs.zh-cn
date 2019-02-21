---
title: 正在加载用户模式显示驱动程序
description: 正在加载用户模式显示驱动程序
ms.assetid: bfebe590-bcde-40cf-9074-8d0f63e0562d
keywords:
- INF 文件 WDK 显示，用户模式驱动程序加载
- 用户模式显示驱动程序 WDK Windows Vista 中，加载
- 加载驱动程序 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81932134fbd1d5f3500ac576a3bc0703dd19f72a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541040"
---
# <a name="loading-a-user-mode-display-driver"></a>正在加载用户模式显示驱动程序


以便在驱动程序安装过程中用户模式显示驱动程序的 DLL 名称添加到注册表，以便 Microsoft Direct3D 运行时可以随后加载 DLL，必须添加注册表部分中的 INF 文件设置以下条目：

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDriverName,    %REG_MULTI_SZ%, Xxx.dll
```

INF 文件必须包含信息以指示要将用户模式显示驱动程序复制到系统的 %systemroot%的操作系统\\system32 目录。 有关详细信息，请参阅[ **INF CopyFiles 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346)并[ **INF DestinationDirs 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547383)。

Direct3D 运行时从注册表中获取用户模式显示驱动程序的 DLL 名称，以便加载运行时的进程空间中的用户模式显示驱动程序。

 

 





