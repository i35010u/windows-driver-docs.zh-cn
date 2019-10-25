---
title: 验证网络配置文件扩展
description: 验证网络配置文件扩展
ms.assetid: d29805a3-7ecb-4587-99c5-b1f8ad9f1503
keywords:
- 网络配置文件 WDK 本机 802.11 IHV 扩展 DLL，验证扩展
- 验证网络配置文件扩展 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa128eb19305deaf2c31035269a4a992bcd8e709
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842963"
---
# <a name="validating-network-profile-extensions"></a>验证网络配置文件扩展




 

在下列情况下，操作系统会调用 IHV 处理程序函数来验证 IHV 定义的连接和安全设置。

-   用户创建新的网络配置文件，该配置文件包含 IHV 定义的连接和/或安全配置文件扩展的设置。 在这种情况下，操作系统将调用[*Dot11ExtIhvValidateProfile*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_validate_profile) IHV 处理程序函数来验证用户设置。

-   WLAN 适配器完成扫描操作，并将其结果返回到操作系统。 操作系统调用[*Dot11ExtIhvPerformCapabilityMatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match) IHV 处理程序函数来确定检测到的基本服务集（BSS）网络是否与网络配置文件中由 IHV 定义的连接和安全设置匹配。

    操作系统将来自 BSS 网络的802.11 信标和探测响应帧的列表传递给**Dot1ExtIhvPerformCapabilityMatch**函数的*pConnectableBssid*参数。 操作系统还会分别向*pIhvConnProfile*和*pIhvSecProfile*参数传递连接和安全配置文件扩展。

    如果802.11 信标和探测响应帧列表中的所有条目都播发在配置文件片段中定义的连接和安全属性，则[*Dot11ExtIhvPerformCapabilityMatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match)函数将\_成功返回错误。

-   操作系统通过调用[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)函数启动一项预关联操作。 在这种情况下，IHV 扩展 DLL 必须验证连接和安全设置是否有效。 如果设置有效，则函数将返回错误\_"成功"，DLL 会继续进行预关联操作。 否则，该函数返回 Winerror.h 中定义的相应错误代码。

    有关预关联操作的详细信息，请参阅[预关联](pre-association-operations.md)操作。

有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)。

 

 





