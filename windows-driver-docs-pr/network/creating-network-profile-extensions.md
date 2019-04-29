---
title: 创建网络配置文件扩展
description: 创建网络配置文件扩展
ms.assetid: b5f7a057-28bc-4df9-99da-58d39b81fb60
keywords:
- 网络配置文件 WDK 本机 802.11 IHV 扩展 DLL，创建扩展
- 扫描操作 WDK 本机 802.11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7bc1f7f5e30e379989a65a118946c6dc609000f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357275"
---
# <a name="creating-network-profile-extensions"></a>创建网络配置文件扩展




 

基础的无线 LAN (WLAN) 适配器完成扫描操作后，它将返回到操作系统检测到的基本服务集 (BSS) 网络的列表。 操作系统调用[ *Dot11ExtIhvCreateDiscoveryProfiles* ](https://msdn.microsoft.com/library/windows/hardware/ff547445)函数为每个用户已创建的网络配置文件的 BSS 网络。 当调用此函数时，临时连接性和可用于连接到 BSS 网络的安全配置文件片段可以返回 IHV 扩展 DLL。

有关扫描操作的详细信息，请参阅[本机 802.11 扫描操作](native-802-11-scan-operations.md)。

当[ *Dot11ExtIhvCreateDiscoveryProfiles* ](https://msdn.microsoft.com/library/windows/hardware/ff547445)是调用，IHV 扩展 DLL 必须遵循这些准则。

-   操作系统将传递给*pConnectableBssid*参数在最后一次扫描操作期间收到一个 IEEE 802.11 信标和探测响应框架的列表。 此列表的格式设置为 DOT11\_BSS\_条目结构。 在列表中的每个信号或探测响应已发送的具有相同的服务集标识符 (SSID) 的访问点 (AP)。

    **请注意**  For Windows Vista 中，只有在基础结构的基本服务设置 (BSS) 网络 IHV 扩展 DLL 支持。

     

    IHV 扩展 DLL 必须分析每个固定长度的字段长度可变的信息元素 (IEs) 以便创建相应的配置文件片段。

-   连接和安全配置文件片段必须包含有效设置，可用于连接到每个通过引用 BSS 标识符 (BSSIDs) 的 Ap *pConnectableBssid*参数。

-   每个连接和安全配置文件片段包含由 IHV 定义的配置文件扩展的 XML 数据。 配置文件片段中的 XML 数据必须分隔&lt;IHV&gt;并&lt;/IHV&gt;标记。

 

 





