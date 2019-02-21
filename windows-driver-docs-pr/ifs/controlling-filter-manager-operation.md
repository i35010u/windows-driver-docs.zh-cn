---
title: 控制筛选器管理器操作
description: 控制筛选器管理器操作
ms.assetid: 884e6a15-5bfa-41bf-b759-af6e43078fad
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，控制操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b87373d79ec8c9e5c99b85001a1d402040512b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555478"
---
# <a name="controlling-filter-manager-operation"></a>控制筛选器管理器操作


在早于由 REG 控制 Windows Vista 版本的 Windows 上的筛选器管理器操作\_DWORD *AttachWhenLoaded*注册表值都存储在以下项：

```cpp
HKLM\System\CurrentControlSet\Services\FltMgr
```

当*AttachWhenLoaded*设置为零，筛选器管理器未附加到的任何卷之前微筛选器驱动程序注册到筛选器管理器。 当*AttachWhenLoaded*设置为 1，筛选器管理器将启动时，所有卷。

默认值为*AttachWhenLoaded*为与 Windows XP Service Pack 2 (SP2) 和更高版本的零。

默认值为*AttachWhenLoaded* Windows Server 2003 Service Pack 1 (SP1) 和更高版本上为 1。

*AttachWhenLoaded*注册表值不存在 Windows Vista 上，仅适用于以前版本的 Windows。

软件安装程序在 Windows Vista 之前的 Windows 上安装微筛选器驱动程序时，应设置*AttachWhenLoaded*为 1，如果此注册表值不当前设置为 1。 如果以前的值*AttachWhenLoaded*是零，安装程序应微筛选器驱动程序的安装后重新启动系统。

 

 




