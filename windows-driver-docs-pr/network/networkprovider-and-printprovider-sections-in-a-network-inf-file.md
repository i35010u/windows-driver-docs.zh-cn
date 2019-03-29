---
title: 网络 INF 文件中的 NetworkProvider 和 PrintProvider 节
description: 网络 INF 文件中的 NetworkProvider 和 PrintProvider 节
ms.assetid: 9ce32644-2b11-4c03-9743-d678ff8de229
keywords:
- INF 文件 WDK 网络，PrintProvider 部分
- 可使用网络 INF 文件 WDK，PrintProvider 部分
- INF 文件 WDK 网络，NetworkProvider 部分
- 可使用网络 INF 文件 WDK，NetworkProvider 部分
- PrintProvider 部分 WDK 网络
- NetworkProvider 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23e57b7f747f1ca25cd5c0c8738febc77dbc5b0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563431"
---
# <a name="networkprovider-and-printprovider-sections-in-a-network-inf-file"></a>网络 INF 文件中的 NetworkProvider 和 PrintProvider 节





**NetClient**组件被视为要网络提供商，因为它们提供网络服务添加到用户应用程序。 网络和 NetWare 客户端的 Microsoft 客户端都属于**NetClient**组件。

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

网络提供商，除了**NetClient**组件还可以打印提供程序。 打印提供程序通过网络提供打印服务添加到用户应用程序。

一个**NetClient**组件始终安装为网络提供商。 安装一个 INF 文件**NetClient**组件除非至少一个以下，则返回 true，否则不要求 NetworkProvider 部分对该组件：

-   为组件指定了可选设备名称。

-   用于指定该组件的短名称**net 视图**命令。 有关详细信息，请参阅[包括 NetworkProvider 部分](including-a-networkprovider-section.md)。

安装 INF **NetClient**组件，它是打印提供程序必须包含**PrintProvider**组件的部分。 有关详细信息，请参阅[包括 PrintProvider 部分](including-a-printprovider-section.md)。

安装一个 INF 文件**NetClient**组件还必须包含*添加注册表部分*(通过引用**AddReg**指令*服务安装部分*组件)，它将**NetworkProvider**到组件的关键**服务**密钥。 有关详细信息，请参阅[NetClient 组件的指定名称和提供程序路径](specifying-the-name-and-provider-path-for-a-netclient-component.md)。

 

 





