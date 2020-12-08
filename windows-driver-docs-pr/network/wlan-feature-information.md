---
title: WLAN 功能信息
description: 本部分包含特定的 WLAN 功能信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddb25cf51f9f87bc5c13e25ce8a255666424e4f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836207"
---
# <a name="wlan-feature-information"></a>WLAN 功能信息


本部分包含特定的 WLAN 功能信息。

## <a name="wi-fi-network-preference"></a>Wi-Fi 网络首选项


Wi-Fi 网络首选项如下所示。

1.  首先使用用户定义的网络。 这些列在 "Wi-Fi CPL" 中作为 *已知网络* 列出。 在以下情况下，网络将成为 *已知网络* 。

    -   用户在网络上手动点击 (包括) Wi-Fi CPL 中的热点。

    -   用户手动从 Wi-Fi CPL 添加网络。

    -   从 Windows 电脑漫游到手机的无线网络配置文件。

    如果在网络扫描期间发现多个用户定义的网络，则使用最近连接的网络。

    **注意**  
    在手机连接到网络一次后，从 Windows 电脑漫游到手机的无线网络配置文件不会显示在 " *已知网络* " 列表中。

     

2.  接下来，将优先使用应用商店应用程序或 OEM 插件)  (的热点。 如果找到多个热点，则使用以下因素来决定首选项。

    -   网络安全。 安全网络 (任何安全类型都是打开的网络的首选) 。

    -   信号强度。

**注意**  
如果有多个网络具有相同的名称或 SSID，则只接受使用该名称或 SSID 的第一个已配置网络。 

如果网络中的信号仍然存在，则 Windows 不会断开与网络的连接，即使更喜欢的网络可用也是如此。 例如，如果用户在商店连接到移动运营商热点，并走回家，而来自热点的信号仍然存在，则电话不会移动到用户配置的 "家庭 Wi-Fi 网络"。

## <a name="also-in-this-section"></a>同时本节还包括：

-   [使用 802.11k、802.11v 和 802.11r 的快速漫游](fast-roaming-with-802-11k--802-11v--and-802-11r.md)
