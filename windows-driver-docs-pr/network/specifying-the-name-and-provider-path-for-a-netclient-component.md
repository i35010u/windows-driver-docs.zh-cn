---
title: 指定 NetClient 组件的名称和提供程序路径
description: 指定 NetClient 组件的名称和提供程序路径
ms.assetid: 4c9c2162-8e7e-44dc-a97c-81074071664b
keywords:
- 添加注册表部分 WDK 网络、 NetClient 组件名称和路径
- NetClient 组件名称和路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78a1100794641c826466c159a58c44d15014b8a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388127"
---
# <a name="specifying-the-name-and-provider-path-for-a-netclient-component"></a>指定 NetClient 组件的名称和提供程序路径





安装 NetClient 组件的 INF 文件必须添加**NetworkProvider**关键*服务*关键组件。 INF 文件将添加**NetworkProvider**密钥通过*添加注册表部分*引用**AddReg**指令*服务安装*组件部分。

**NetworkProvider**密钥有两个值：**名称**指定的网络提供商，名称和一个**ProviderPath** ，它指定到网络的完整路径提供程序 DLL。

以下是一种*添加注册表部分*，它将**NetworkProvider**密钥与该实例键的组件：

```INF
[NWCWorkstation.AddReg]
HKR, NetworkProvider, Name, 0, "NetWare or Compatible Network"
HKR, NetworkProvider, ProviderPath, 0x20000, "%11%\nwprovau.dll"
```

**请注意**  安装的 INF 文件**NetClient**组件无需更新**ProviderOrder**下组件的值...**控件\\网络\\提供程序\\顺序**密钥。 这是自动通过网络类安装程序。

 

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

 

 





