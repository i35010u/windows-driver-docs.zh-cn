---
title: 使用 802.11k、802.11v 和 802.11r 的快速漫游
description: 本部分介绍了通过 802.11 k、801.11 v 和 802.11 r 进行的 WLAN 漫游体验改进
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c3853a2de599fdcc9002bd686c7e6facd689ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837207"
---
# <a name="fast-roaming-with-80211k-80211v-and-80211r"></a>使用 802.11k、802.11v 和 802.11r 的快速漫游


现在可在运行 Windows 10 的设备上使用更高的 WLAN 漫游体验。 一种行业标准实现，可缩短设备从一个无线接入点 (AP) 漫游所需的时间。

## <a name="80211k-neighbor-reports"></a>802.11 k (邻居报告) 


支持 802.11 k (Ap) 的无线访问点能够向运行 Windows 10 的设备提供邻居报告。 邻居报表包含有关邻近访问点的信息，并允许设备更好地了解其环境。 Windows 10 利用此功能，因为在查找要漫游到的邻近 AP 之前，会缩短设备需要扫描的通道的列表。

## <a name="80211v-bss-transition-management-frames"></a>802.11 v (BSS 转换管理框架) 


支持 802.11 v 的 Ap 现在可以将 Windows 10 设备定向到其认为将为设备提供更好的 WLAN 体验的其他 AP。 Windows 10 设备现在可以接受并响应 (BSS) 转换管理框架的基本服务集，从而在连接到支持 802.11 v 的网络时提高了 WLAN 质量。

## <a name="80211r-fast-bss-transition"></a>802.11 r (快速 BSS 转换) 


快速 BSS 转换缩短了 Windows 10 设备转换为支持 802.11 r 的 AP 所需的时间。 这一时间减少了在传输数据前将与 AP 交换的帧更少的结果。 通过在设备从一个 AP 漫游到另一个 AP 时，减少数据传输前的时间，可提高延迟敏感的应用程序（例如活动 Skype 呼叫）的连接质量。 Windows 10 支持通过使用 802.1 X 的网络进行快速 BSS 转换，作为身份验证方法。 当前不支持 (PSK) 和开放网络的预共享密钥。

结合使用 802.11 k、802.11 v 和 802.11 r，Windows 10 利用了既定的行业标准来改善用户的漫游体验。 VoIP 应用程序现在可以利用这一改进的漫游功能，在用户不是静止的情况下提供更好的呼叫质量。

## <a name="things-to-note"></a>需要注意的事项


并非所有 Windows 10 设备都支持 802.11 k、802.11 v 和 802.11 r。 WLAN 无线电驱动程序必须支持这些功能才能在 Windows 10 上运行。 请咨询你的设备制造商，确定你的设备是否支持这些功能。 除了设备端支持外，网络 (AP 控制器和 Ap) 还必须支持功能才能工作。 请与网络管理员联系，以了解这些功能是否受支持，并在有问题的网络上启用了这些功能。

当设备或网络上没有 802.11 r 可用时，Windows 10 继续支持机会密钥缓存 (OKC) 。

这三种功能都需要 AP 端支持，且在未在 Ap 上启用这些功能的情况下将无法运行。

 

 





