---
title: 无线网络配置文件的扩展属性
description: 无线网络配置文件的扩展属性
ms.assetid: c98266b5-3841-4dfa-b274-5c1ef16bfef6
keywords:
- IHV UI 扩展 DLL WDK 本机 802.11，网络配置文件扩展
- 网络配置文件 WDK 本机 802.11 IHV UI 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e053ab00c146956b6e66f347ae4b8228c3ebc0ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546919"
---
# <a name="extending-the-properties-for-wireless-network-profiles"></a>无线网络配置文件的扩展属性




 

最终用户创建或编辑通过本机 802.11 网络配置用户界面 (UI) 的无线网络连接配置文件。 关于此用户界面的详细信息，请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)。

独立硬件供应商 (IHV) 可以扩展以支持通过本机 802.11 UI 扩展 DLL 专有连接和安全配置文件设置将网络配置 UI。 该 DLL 可以扩展网络配置 UI 中显示以下选项卡。

<a href="" id="connection-tab"></a>**连接选项卡**  
此选项卡显示用于无线局域网 (WLAN) 网络的连接设置的用户界面。

本机 802.11 IHV UI 扩展 DLL 可以扩展此 UI 中所述的过程[扩展无线连接属性页](extending-wireless-connection-properties.md)。

**请注意**  For Windows Vista 中，本机 802.11 UI 扩展 DLL 只能支持一个扩展**连接**选项卡。

 

<a href="" id="security-tab-------"></a>**安全选项卡**   
此选项卡显示用于无线局域网 (WLAN) 网络的安全设置的用户界面。

本机 802.11 IHV UI 扩展 DLL 可以通过添加显示元素的专用安全设置扩展此 UI。 有关此过程的详细信息，请参阅[扩展无线安全属性页](extending-wireless-security-properties.md)。

本机 802.11 IHV UI 扩展 DLL 还可以扩展 Microsoft 802.1 X 设置上**安全**选项卡。有关此过程的详细信息，请参阅[扩展 Microsoft 802.1 X 安全设置](extending-microsoft-802-1x-security-settings.md)。

**请注意**  For Windows Vista 中，本机 802.11 IHV UI 扩展 DLL 只能扩展的基础结构无线网络连接和安全配置文件的属性。

 

 

 





