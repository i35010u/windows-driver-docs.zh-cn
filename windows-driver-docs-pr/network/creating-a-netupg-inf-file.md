---
title: 创建 Netupg.inf 文件
description: 创建 Netupg.inf 文件
keywords:
- netupg 文件 WDK
- 网络组件升级 WDK，自定义
- 升级网络组件 WDK，自定义
- 自定义网络升级过程 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1874bc4f3e2c867250a98b0b99e44a34f9d2060
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822217"
---
# <a name="creating-a-netupginf-file"></a>创建 Netupg.inf 文件





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

Netupg 文件包含名为 **OemNetUpgradeDirs** 的单个部分。 此部分中的每个条目指定一个目录的完整路径，该目录包含供应商提供的非 Microsoft 支持的网络组件升级文件。 要升级的每个网络组件在 **OemNetUpgradeDirs** 节中必须有对应的条目。

下面是 netupg 文件的一个示例：

```INF
[OemNetUpgradeDirs]
c:\temp\adapter1
c:\temp\adapter2
c:\temp\protocol1
c:\temp\netclient1
c:\temp\netservice1
```

在 **OemNetUpgradeDirs** 节中指定的每个目录都必须包含一个 netmap 文件。 此文件由网络组件的供应商提供，将网络组件的 preupgrade 设备、硬件或兼容 ID 映射到升级后的操作系统中相应的 ID。

 

 





