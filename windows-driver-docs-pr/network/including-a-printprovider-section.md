---
title: 包含 PrintProvider 节
description: 包含 PrintProvider 节
keywords:
- INF 文件 WDK network，PrintProvider 部分
- 网络 INF 文件 WDK，PrintProvider 部分
- PrintProvider 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53e95f4f50f8713339252af4566f1af2adece567
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821311"
---
# <a name="including-a-printprovider-section"></a>包含 PrintProvider 节





安装作为打印提供程序的 **NetClient** 组件的 INF 文件必须包含该组件的 **PrintProvider** 部分。

**请注意**，**NetClient** 组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  

 

若要创建 **PrintProvider** 节，请将 **PrintProvider** 扩展添加到组件的 *DDInstall* 节，如以下示例中所示：
```cpp
[DDInstall-section] ; Install section
[DDInstall-section.PrintProvider] ; PrintProvider section
```

**PrintProvider** 部分必须包含以下条目：

<a href="" id="printprovidername"></a>**PrintProviderName**  
指定打印提供程序的名称的非本地化字符串。

<a href="" id="printproviderdll"></a>**PrintProviderDll**  
打印提供程序 DLL 的文件名。

<a href="" id="displayname"></a>**DisplayName**  
一个可本地化的字符串，它指定打印提供程序的名称。 **DisplayName** 可不同于 **PrintProviderName**。

**PrintProviderName** 和 **PrintProviderDll** 项提供的信息可用作 PROVIDOR \_ INFO \_ 1 结构) 到 **AddPrintProvidor** 函数的输入 (。 **AddPrintProvidor** 函数将打印提供程序组件作为打印提供程序添加。 有关 **AddPrintProvidor** 函数的详细信息，请参阅 Microsoft Windows SDK。

下面是 **PrintProvider** 部分的示例：

```cpp
[DDnstall-section.PrintProvider]
PrintProviderName = "NetWare or Compatible Network"
PrintProviderDll  = "nwprovau.dll"
DisplayName       = "%NWC_Network_Display_Name%"
```

 

 





