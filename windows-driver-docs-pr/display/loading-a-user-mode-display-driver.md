---
title: 加载用户模式显示驱动程序
description: 加载用户模式显示驱动程序
ms.assetid: bfebe590-bcde-40cf-9074-8d0f63e0562d
keywords:
- INF 文件 WDK 显示，用户模式驱动程序加载
- 用户模式显示驱动程序 WDK Windows Vista 中，加载
- 加载驱动程序 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a923ee29e3a66ad071ccfb96e5ff1e143d05fcc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380382"
---
# <a name="loading-a-user-mode-display-driver"></a>加载用户模式显示驱动程序


以便在驱动程序安装过程中用户模式显示驱动程序的 DLL 名称添加到注册表，以便 Microsoft Direct3D 运行时可以随后加载 DLL，必须添加注册表部分中的 INF 文件设置以下条目：

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDriverName,    %REG_MULTI_SZ%, Xxx.dll
```

INF 文件必须包含信息以指示要将用户模式显示驱动程序复制到系统的 %systemroot%的操作系统\\system32 目录。 有关详细信息，请参阅[ **INF CopyFiles 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)并[ **INF DestinationDirs 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)。

Direct3D 运行时从注册表中获取用户模式显示驱动程序的 DLL 名称，以便加载运行时的进程空间中的用户模式显示驱动程序。

 

 





