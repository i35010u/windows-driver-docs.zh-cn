---
title: 本机 802.11 IHV UI 扩展 DLL 概述
description: 本机 802.11 IHV UI 扩展 DLL 概述
keywords:
- IHV UI 扩展 DLL WDK 本机802.11，关于 IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acd13460419c869fad0155493a6dbd9d68729167
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798057"
---
# <a name="native-80211-ihv-ui-extensions-dll-overview"></a>本机 802.11 IHV UI 扩展 DLL 概述




 

如果独立硬件供应商 (IHV) 提供本机 802.11 IHV 扩展 DLL，则 IHV 可以选择提供本机 802.11 IHV UI 扩展 DLL。 通过此 DLL，IHV 可以执行以下操作：

-   扩展 Microsoft 网络配置用户界面 (UI) 属性，这些属性用于无线连接和安全配置设置。 在这种情况下，本机 802.11 IHV UI 扩展 DLL 可以执行以下操作：

    -   向标准 Microsoft 802.11 属性添加自定义显示元素。 例如，本机 802.11 IHV UI 扩展 DLL 可以向列表中添加项，以向最终用户提供专用安全选项的选择。
    -   启动可用于配置专用连接和安全设置的自定义 UI。

    有关扩展 Microsoft 802.11 属性的详细信息，请参阅 [扩展801.11 属性](extending-the-properties-for-wireless-network-profiles.md)。

-   在本机 802.11 IHV 扩展 DLL 的请求中启动自定义 UI。 根据基础本机802.11 微型端口驱动程序的当前状态，操作系统会将 UI 显示为以下内容之一：

    -   操作系统的 802.11 UI 流内的一组向导页面。 例如，如果本机 802.11 IHV 扩展 DLL 在无线局域网 (WLAN) 连接操作期间需要用户凭据，则操作系统会显示由本机 802.11 UI 扩展 DLL 提供的自定义 UI 页面，作为标准 UI 流的一部分。

        从气球通知启动的独立 UI。 例如，如果本机802.11 扩展 DLL 确定 WLAN 连接上的连接或身份验证状态已更改，则 DLL 可以请求本机 802.11 UI 扩展 DLL 显示气球通知以提醒最终用户。

    若要详细了解如何启动来自本机802.11 扩展 DLL 请求的 UI，请参阅 [处理来自本机 802.11 IHV 扩展 dll 的 Ui 请求](handling-requests-for-the-display-of-a-custom-ui.md)。

有关本机 802.11 IHV 扩展 DLL 的详细信息，请参阅 [本机 802.11 Ihv 扩展 dll](native-802-11-ihv-extensions-dll4.md)。

有关 Microsoft 网络配置 UI 和其他本机802.11 组件的详细信息，请参阅 [本机802.11 软件体系结构](/previous-versions/windows/hardware/wireless/native-802-11-software-architecture)。

 

 
