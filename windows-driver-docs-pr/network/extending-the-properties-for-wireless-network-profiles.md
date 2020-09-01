---
title: 扩展无线网络配置文件的属性
description: 扩展无线网络配置文件的属性
ms.assetid: c98266b5-3841-4dfa-b274-5c1ef16bfef6
keywords:
- IHV UI 扩展 DLL WDK 本机802.11，网络配置文件扩展
- 网络配置文件 WDK 本机 802.11 IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38f130c2808f6501d3779598d18bc963db04ffe9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212929"
---
# <a name="extending-the-properties-for-wireless-network-profiles"></a>扩展无线网络配置文件的属性




 

最终用户通过本机802.11 网络配置用户界面 (UI) 创建或编辑无线网络连接配置文件。 有关此 UI 的详细信息，请参阅 [本机802.11 软件体系结构](/previous-versions/windows/hardware/wireless/native-802-11-software-architecture)。

独立硬件供应商 (IHV) 可以扩展网络配置 UI，以支持通过本机 802.11 UI 扩展 DLL 提供的专用连接和安全配置文件设置。 DLL 可以扩展网络配置 UI 中显示的以下选项卡。

<a href="" id="connection-tab"></a>**连接选项卡**  
此选项卡显示无线 LAN (WLAN) 网络的连接设置的 UI。

本机 802.11 IHV UI 扩展 DLL 可以按照 [扩展无线连接属性页](extending-wireless-connection-properties.md)中所述的过程来扩展此 UI。

**注意**   对于 Windows Vista，本机 802.11 UI 扩展 DLL 只能支持一个到 "**连接**" 选项卡的扩展。

 

<a href="" id="security-tab-------"></a>**安全选项卡**   
此选项卡显示 (WLAN) 网络的无线 LAN 安全设置的 UI。

本机 802.11 IHV UI 扩展 DLL 可以通过添加专用安全设置的显示元素来扩展此 UI。 有关此过程的详细信息，请参阅 [扩展无线安全属性页](extending-wireless-security-properties.md)。

本机 802.11 IHV UI 扩展 DLL 还可以在 " **安全** " 选项卡上扩展 Microsoft 802.1 x 设置。有关此过程的详细信息，请参阅 [扩展 Microsoft 802.1 x 安全设置](extending-microsoft-802-1x-security-settings.md)。

**注意**   对于 Windows Vista，本机 802.11 IHV UI 扩展 DLL 只能扩展基础结构无线网络的连接和安全配置文件的属性。

 

 

 