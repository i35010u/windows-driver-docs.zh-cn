---
title: 指定 NetClient 组件的名称和提供程序路径
description: 指定 NetClient 组件的名称和提供程序路径
keywords:
- 添加-注册表--WDK 网络，NetClient 组件名称和路径
- NetClient 组件名称和路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43d45652c1c12fe9828ef4f610627d7b42b22295
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815867"
---
# <a name="specifying-the-name-and-provider-path-for-a-netclient-component"></a>指定 NetClient 组件的名称和提供程序路径





安装 NetClient 组件的 INF 文件必须在组件的 *服务* 密钥中添加 **NetworkProvider** 键。 INF 文件通过在组件的 *服务安装* 部分引用的 " **NetworkProvider** "*部分添加* 了 " **AddReg** " 指令。

**NetworkProvider** 键具有两个值：指定网络提供程序的名称的 **名称**，以及指定网络提供程序 DLL 的完整路径的 **ProviderPath** 。

下面是 *添加注册表部分* 的一个示例，它将 **NetworkProvider** 键添加到组件的实例键：

```INF
[NWCWorkstation.AddReg]
HKR, NetworkProvider, Name, 0, "NetWare or Compatible Network"
HKR, NetworkProvider, ProviderPath, 0x20000, "%11%\nwprovau.dll"
```

**注意**  安装 **NetClient** 组件的 INF 文件不需要更新组件 ... 下的 **ProviderOrder** 值。 **控件 \\网络 \\ 提供商 \\ 顺序** 键。 网络类安装程序会自动完成此操作。

 

**请注意**，**NetClient** 组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  

 

 

 





