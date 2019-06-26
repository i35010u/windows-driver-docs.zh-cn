---
title: 验证网络配置文件扩展
description: 验证网络配置文件扩展
ms.assetid: d29805a3-7ecb-4587-99c5-b1f8ad9f1503
keywords:
- 网络配置文件 WDK 本机 802.11 IHV 扩展 DLL，验证扩展插件
- 验证网络配置文件扩展 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e46953bcff1b4032b0d0f3891a3567aad2bd2a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384362"
---
# <a name="validating-network-profile-extensions"></a>验证网络配置文件扩展




 

操作系统将调用 IHV 处理程序函数来验证以下条件下 IHV 定义连接和安全的设置。

-   用户创建新的网络配置文件包含 IHV 定义连接和/或安全配置文件扩展插件的设置。 在此情况下，操作系统将调用[ *Dot11ExtIhvValidateProfile* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_validate_profile) IHV 处理程序函数来验证用户设置。

-   将 WLAN 适配器完成扫描操作，并将其结果返回给操作系统。 操作系统调用[ *Dot11ExtIhvPerformCapabilityMatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match) IHV 处理程序函数来确定网络是否检测到的基本服务设置 (BSS) 匹配的 IHV 定义连接和从网络配置文件的安全设置。

    操作系统将从 BSS 网络传递一系列 802.11 信标和探测响应帧*pConnectableBssid*的参数**Dot1ExtIhvPerformCapabilityMatch**函数。 操作系统还会传递连接和安全配置文件的扩展*pIhvConnProfile*并*pIhvSecProfile*参数，分别。

    如果 802.11 信标和探测响应帧列表中的项的所有播发配置文件片段中定义的连接和安全属性[ *Dot11ExtIhvPerformCapabilityMatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match)函数将返回错误\_成功。

-   操作系统启动预关联操作通过调用[ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)函数。 在此情况下，IHV 扩展 DLL 必须验证的连接和安全设置有效。 如果设置是否有效，该函数将返回错误\_成功和 DLL 将继续进行预关联操作。 否则，该函数返回相应的错误代码在 Winerror.h 中定义。

    有关预关联操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)。

 

 





