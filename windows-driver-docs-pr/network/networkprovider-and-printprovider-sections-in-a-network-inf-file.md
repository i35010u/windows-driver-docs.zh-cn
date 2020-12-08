---
title: 网络 INF 文件中的 NetworkProvider 和 PrintProvider 节
description: 网络 INF 文件中的 NetworkProvider 和 PrintProvider 节
keywords:
- INF 文件 WDK network，PrintProvider 部分
- 网络 INF 文件 WDK，PrintProvider 部分
- INF 文件 WDK network，NetworkProvider 部分
- 网络 INF 文件 WDK，NetworkProvider 部分
- PrintProvider 部分 WDK 网络
- NetworkProvider 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08b6dc7ddee99d4cb245a950c08cd78bccaa4eb1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834363"
---
# <a name="networkprovider-and-printprovider-sections-in-a-network-inf-file"></a>网络 INF 文件中的 NetworkProvider 和 PrintProvider 节





**NetClient** 组件被视为网络提供程序，因为它们向用户应用程序提供网络服务。 适用于网络的 Microsoft 客户端和 NetWare 客户端是 **NetClient** 组件的示例。

**请注意**，**NetClient** 组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  

 

除了作为网络提供程序外， **NetClient** 组件还可以是打印提供程序。 打印提供程序通过网络将打印服务提供给用户应用程序。

**NetClient** 组件始终作为网络提供程序安装。 除非至少满足以下条件之一，否则安装 **NetClient** 组件的 INF 文件不需要该组件的 NetworkProvider 部分：

-   为组件指定了备用设备名称。

-   指定组件的短名称用于 **net view** 命令。 有关详细信息，请参阅 [包含 NetworkProvider 部分](including-a-networkprovider-section.md)。

安装作为打印提供程序的 **NetClient** 组件的 INF 必须包含该组件的 **PrintProvider** 部分。 有关详细信息，请参阅 [包含 PrintProvider 部分](including-a-printprovider-section.md)。

安装 **NetClient** 组件的 INF 文件还必须包含 "" 部分中的 **AddReg** 指令引用的 "*添加注册表" 部分* (*，该组件*) 将 **NetworkProvider** 项添加到组件的 **服务** 密钥。 有关详细信息，请参阅 [指定 NetClient 组件的名称和提供程序路径](specifying-the-name-and-provider-path-for-a-netclient-component.md)。

 

 





