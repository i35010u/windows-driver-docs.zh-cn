---
title: 控制筛选器管理器操作
description: 控制筛选器管理器操作
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，控制操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dc452e6cc8726aa3c6b324a367106333db3b7e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840101"
---
# <a name="controlling-filter-manager-operation"></a>控制筛选器管理器操作


早于 Windows Vista 的 Windows 版本上的筛选器管理器的操作由注册表中的 \_ 注册表值 *AttachWhenLoaded* 注册表值控制，该注册表值存储在以下注册表项中：

```cpp
HKLM\System\CurrentControlSet\Services\FltMgr
```

当 *AttachWhenLoaded* 设置为零时，筛选器将不会附加到任何卷，除非微微筛选器驱动程序向筛选器管理器注册。 当 *AttachWhenLoaded* 设置为1时，筛选器管理器将在启动时附加到所有卷。

默认情况下， *AttachWhenLoaded* 的默认值为零，Windows XP Service Pack 2 (SP2) 和更高版本。

Windows Server 2003 上的 *AttachWhenLoaded* 的默认值为1，Service Pack 1 (SP1) 和更高版本。

*AttachWhenLoaded* 注册表值不存在于 windows Vista 上，并且仅适用于以前版本的 windows。

如果在 windows Vista 之前的 Windows 上安装了微筛选器驱动程序，则如果此注册表值当前未设置为1，则软件安装程序应将 *AttachWhenLoaded* 设置为1。 如果以前的 *AttachWhenLoaded* 值为零，则安装程序将在安装微筛选器驱动程序后重新启动系统。

 

 




