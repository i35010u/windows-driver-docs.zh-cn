---
title: 使用 802.11k、802.11v 和 802.11r 的快速漫游
description: 本部分介绍了漫游 802.11 k、 801.11v，与 802.11r 体验的改进的 WLAN
ms.assetid: EAD532E7-7C43-45BF-8C1A-5645A15F2607
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39ac378f9629304f3f234af5c9f3ee752a586a93
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568887"
---
# <a name="fast-roaming-with-80211k-80211v-and-80211r"></a>使用 802.11k、802.11v 和 802.11r 的快速漫游


改进了的 WLAN 漫游体验目前可供运行 Windows 10 的设备。 现在支持，使设备能够从一个无线访问点 (AP) 漫游所需的时间减少到另一个的行业标准实现。

## <a name="80211k-neighbor-reports"></a>802.11 k （邻居报表）


支持 802.11 k 的无线访问点 (Ap) 都能够向运行 Windows 10 的设备提供相邻的报表。 相邻报表包含有关相邻的访问点的信息，并允许设备以实现更好地了解其环境。 Windows 10 通过缩短在设备需要扫描才能找到一个相邻 AP 漫游到的频道列表会利用此功能。

## <a name="80211v-bss-transition-management-frames"></a>802.11v （BSS 转换管理框架）


支持 802.11v APs 现在可以直接漫游到另一个它认为将为设备提供更好的 WLAN 体验的亚太的 Windows 10 设备。 Windows 10 设备现在可以接受并响应这些基本服务设置 (BSS) 转换管理框架，从而导致改进 WLAN 质量时连接到支持 802.11v 的网络。

## <a name="80211r-fast-bss-transition"></a>802.11r （快速 BSS 转换）


快速 BSS 转换可以减少支持 802.11r 的接入点转换为 Windows 10 设备所需的时间。 此时间缩短得出更少的帧与数据传输之前 AP 正进行交换。 通过减少数据传输时从一个 AP 漫游到另一个的设备前的时间，连接质量改进延迟敏感的应用程序，如活动的 Skype 调用。 Windows 10 支持的身份验证方法使用 802.1x 网络上快速 BSS 转换。 当前不支持预共享密钥 (PSK) 和开放网络。

802.11 k、 802.11v 和 802.11r 相结合，与 Windows 10 充分利用已建立的行业标准来改进我们的用户的漫游体验。 VoIP 的应用程序现在可以充分利用此改进了漫游，以提供更好地调用质量时用户不是固定的。

## <a name="things-to-note"></a>需要注意的事项


并非所有 Windows 10 设备都支持 802.11 k、 802.11v 和 802.11r。 WLAN 单选驱动程序必须支持这些功能，使其可在 Windows 10 上。 请咨询设备制造商联系，以确定你的设备支持这些功能。 除了设备端支持网络 （AP 控制器和 APs） 还必须支持丰富的经验来工作的功能。 请与网络管理员联系以了解是否这些功能支持和相关网络上启用了。

Windows 10 继续 802.11r 不可用的设备或网络上时支持机会密钥缓存 (OKC)。

所有三个功能需要端亚太的支持，并且未接入点上启用这些功能将无法工作。

 

 





