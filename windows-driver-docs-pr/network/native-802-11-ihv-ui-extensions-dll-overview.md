---
title: 本机 802.11 IHV UI 扩展 DLL 概述
description: 本机 802.11 IHV UI 扩展 DLL 概述
ms.assetid: 82276ffb-eec4-4a77-9feb-f8f2ca1d7b34
keywords:
- IHV UI 扩展 DLL WDK 本机 802.11 有关 IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69bcd8157f00cff341cecc4365a40af20ecd7c67
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344235"
---
# <a name="native-80211-ihv-ui-extensions-dll-overview"></a>本机 802.11 IHV UI 扩展 DLL 概述




 

如果独立硬件供应商 (IHV) 提供了本机 802.11 IHV 扩展 DLL，IHV 可以选择提供本机 802.11 IHV UI 扩展 DLL。 通过此 DLL，IHV 可以执行以下操作：

-   扩展 Microsoft 网络配置用户界面 (UI) 属性，用于无线连接和安全配置设置。 在此情况下，本机 802.11 IHV UI 扩展 DLL 可以执行以下步骤：

    -   将自定义显示元素添加到标准的 Microsoft 802.11 属性。 例如，本机 802.11 IHV UI 扩展 DLL 可以将项添加到一个列表，用于向最终用户提供选择专有的安全选项之一。
    -   启动一个自定义 UI，可用于配置专用连接和安全设置。

    有关将 Microsoft 802.11 属性扩展的详细信息，请参阅[扩展 801.11 属性](extending-the-properties-for-wireless-network-profiles.md)。

-   启动本机 802.11 IHV 扩展 DLL 的要求自定义 UI。 根据基础本机 802.11 微型端口驱动程序的当前状态，操作系统会显示用户界面为以下任一：

    -   一系列的操作系统的 802.11 UI 流中的向导页。 例如，如果本机 802.11 IHV 扩展 DLL 无线 LAN (WLAN) 连接操作期间需要用户凭据，操作系统会显示由本机 802.11 UI 扩展 DLL 作为标准 UI 流的一部分提供的自定义 UI 页面。

        从气球状通知启动独立 UI。 例如，如果本机 802.11 扩展 DLL 确定 WLAN 连接上的连接或身份验证状态已更改，该 DLL 可以请求本机 802.11 UI 扩展 DLL 显示气球状通知最终用户发出警报。

    有关启动来自本机 802.11 扩展 DLL 的请求而得出的 UI 的详细信息，请参阅[本机 802.11 IHV 扩展 DLL 从处理 UI 请求](handling-requests-for-the-display-of-a-custom-ui.md)。

有关本机 802.11 IHV 扩展 DLL 的详细信息，请参阅[本机 802.11 IHV 扩展 DLL](native-802-11-ihv-extensions-dll4.md)。

有关 Microsoft 网络配置 UI 和其他本机 802.11 组件的详细信息，请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)。

 

 





