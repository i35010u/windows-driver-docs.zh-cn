---
title: 创建网络配置文件扩展
description: 创建网络配置文件扩展
keywords:
- 网络配置文件 WDK 本机 802.11 IHV 扩展 DLL，创建扩展
- 扫描操作 WDK 本机802.11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02aa152675893cb0f9d460c617130881a6bd2121
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838431"
---
# <a name="creating-network-profile-extensions"></a>创建网络配置文件扩展




 

在基础无线 LAN (WLAN) 适配器完成扫描操作后，它会将检测到的基本服务集的列表（ () BSS）返回到操作系统。 对于用户尚未为其创建网络配置文件的每个 BSS 网络，操作系统将调用 [*Dot11ExtIhvCreateDiscoveryProfiles*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_create_discovery_profiles) 函数。 调用此函数时，IHV 扩展 DLL 可以返回可用于连接到 BSS 网络的临时连接和安全配置文件片段。

有关扫描操作的详细信息，请参阅 [本机802.11 扫描操作](/previous-versions/windows/hardware/wireless/native-802-11-scan-operations)。

调用 [*Dot11ExtIhvCreateDiscoveryProfiles*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_create_discovery_profiles) 时，IHV 扩展 DLL 必须遵循这些准则。

-   操作系统将向 *pConnectableBssid* 参数传递在上一次扫描操作期间接收的 IEEE 802.11 信标和探测响应帧的列表。 此列表的格式为 DOT11 \_ BSS \_ 条目结构。 列表中的每个信标或探测响应都是通过访问点 (AP) 发送的，该接入点具有相同的服务集标识符 (SSID) 。

    **注意**  对于 Windows Vista，IHV 扩展 DLL 仅支持基础结构基本服务集 (BSS) 网络。

     

    若要创建适当的配置文件片段，IHV 扩展 DLL 必须分析每个固定长度的字段和可变长度信息元素 () 。

-   连接和安全配置文件片段必须包含有效的设置，这些设置可用于连接到每个 Ap，其 BSS 标识符 (BSSIDs) 通过 *pConnectableBssid* 参数进行引用。

-   每个连接和安全配置文件片段都包含由 IHV 定义的配置文件扩展的 XML 数据。 配置文件片段中的 XML 数据必须由 &lt; IHV &gt; 和 &lt; /IHV 标记进行分隔 &gt; 。

 

 
