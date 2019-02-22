---
title: 创建 Netupg.inf 文件
description: 创建 Netupg.inf 文件
ms.assetid: 8ee000e0-abd1-4a06-9f38-2a7971bc2c97
keywords:
- netupg.inf 文件 WDK
- 网络组件升级 WDK，自定义
- 升级网络组件 WDK、 自定义
- 自定义网络升级过程 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73b0a899d68714290fa88887ee35c2b902902e7f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542372"
---
# <a name="creating-a-netupginf-file"></a>创建 Netupg.inf 文件





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

Netupg.inf 文件包含一个名为的单个部分**OemNetUpgradeDirs**。 在本部分中的每个条目指定包含非 Microsoft 支持网络组件的供应商提供升级文件的目录的完整路径。 正在升级的每个网络组件必须具有一个对应的条目**OemNetUpgradeDirs**部分。

下面是 netupg.inf 文件的示例：

```INF
[OemNetUpgradeDirs]
c:\temp\adapter1
c:\temp\adapter2
c:\temp\protocol1
c:\temp\netclient1
c:\temp\netservice1
```

中指定每个目录**OemNetUpgradeDirs**部分必须包含一个 netmap.inf 文件。 网络组件的供应商提供，此文件将升级前的设备、 硬件或网络组件的兼容 ID 映射到已升级的操作系统中相应的 ID。

 

 





