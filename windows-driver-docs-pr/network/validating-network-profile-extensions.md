---
title: 验证网络配置文件扩展
description: 验证网络配置文件扩展
ms.assetid: d29805a3-7ecb-4587-99c5-b1f8ad9f1503
keywords:
- 网络配置文件 WDK 本机 802.11 IHV 扩展 DLL，验证扩展插件
- 验证网络配置文件扩展 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52e01b65932935224b6e9f823d3d33fa973758b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368905"
---
# <a name="validating-network-profile-extensions"></a>验证网络配置文件扩展




 

操作系统将调用 IHV 处理程序函数来验证以下条件下 IHV 定义连接和安全的设置。

-   用户创建新的网络配置文件包含 IHV 定义连接和/或安全配置文件扩展插件的设置。 在此情况下，操作系统将调用[ *Dot11ExtIhvValidateProfile* ](https://msdn.microsoft.com/library/windows/hardware/ff547523) IHV 处理程序函数来验证用户设置。

-   将 WLAN 适配器完成扫描操作，并将其结果返回给操作系统。 操作系统调用[ *Dot11ExtIhvPerformCapabilityMatch* ](https://msdn.microsoft.com/library/windows/hardware/ff547488) IHV 处理程序函数来确定网络是否检测到的基本服务设置 (BSS) 匹配的 IHV 定义连接和从网络配置文件的安全设置。

    操作系统将从 BSS 网络传递一系列 802.11 信标和探测响应帧*pConnectableBssid*的参数**Dot1ExtIhvPerformCapabilityMatch**函数。 操作系统还会传递连接和安全配置文件的扩展*pIhvConnProfile*并*pIhvSecProfile*参数，分别。

    如果 802.11 信标和探测响应帧列表中的项的所有播发配置文件片段中定义的连接和安全属性[ *Dot11ExtIhvPerformCapabilityMatch* ](https://msdn.microsoft.com/library/windows/hardware/ff547488)函数将返回错误\_成功。

-   操作系统启动预关联操作通过调用[ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499)函数。 在此情况下，IHV 扩展 DLL 必须验证的连接和安全设置有效。 如果设置是否有效，该函数将返回错误\_成功和 DLL 将继续进行预关联操作。 否则，该函数返回相应的错误代码在 Winerror.h 中定义。

    有关预关联操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](https://msdn.microsoft.com/library/windows/hardware/ff560627)。

 

 





