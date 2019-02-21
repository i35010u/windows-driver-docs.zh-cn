---
title: 包括 PrintProvider 部分
description: 包括 PrintProvider 部分
ms.assetid: 2cbf1b56-e603-4a21-a1d7-d51634c91456
keywords:
- INF 文件 WDK 网络，PrintProvider 部分
- 可使用网络 INF 文件 WDK，PrintProvider 部分
- PrintProvider 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ecd949a2278e56790f3ad9b37f6531bf4362605
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544909"
---
# <a name="including-a-printprovider-section"></a>包括 PrintProvider 部分





安装一个 INF 文件**NetClient**组件，它是打印提供程序必须包含**PrintProvider**组件的部分。

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

若要创建**PrintProvider**部分中，添加**PrintProvider**扩展*DDInstall*部分组件，如下面的示例中所示：
```cpp
[DDInstall-section] ; Install section
[DDInstall-section.PrintProvider] ; PrintProvider section
```

**PrintProvider**部分必须包含以下各项：

<a href="" id="printprovidername"></a>**PrintProviderName**  
一个非本地化的字符串，指定打印提供程序的名称。

<a href="" id="printproviderdll"></a>**PrintProviderDll**  
打印提供程序 DLL 的文件名称。

<a href="" id="displayname"></a>**DisplayName**  
可本地化的字符串，指定打印提供程序的名称。 **DisplayName**可能不同于**PrintProviderName**。

**PrintProviderName**并**PrintProviderDll**条目提供用作输入的信息 (在提供程序\_信息\_1 结构) 到**AddPrintProvidor**函数。 **AddPrintProvidor**函数将作为打印提供程序添加打印提供程序组件。 有关详细信息**AddPrintProvidor**函数中，请参阅 Microsoft Windows SDK。

以下是一种**PrintProvider**部分：

```cpp
[DDnstall-section.PrintProvider]
PrintProviderName = "NetWare or Compatible Network"
PrintProviderDll  = "nwprovau.dll"
DisplayName       = "%NWC_Network_Display_Name%"
```

 

 





