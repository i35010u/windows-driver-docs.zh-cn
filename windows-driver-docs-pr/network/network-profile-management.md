---
title: 网络配置文件管理
description: 网络配置文件管理
keywords:
- IHV 扩展 DLL WDK 本机802.11，网络配置文件
- 网络配置文件 WDK 本机 802.11 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK，网络配置文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 661ec462edf7bfbdf3ba577005c1a08fe8b14b4f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787241"
---
# <a name="network-profile-management"></a>网络配置文件管理




 

本部分介绍如何通过 IHV 扩展 DLL 管理和处理网络配置文件。 网络配置文件定义基本服务 (BSS) 网络的连接操作属性。

IHV 扩展 DLL 负责验证或创建网络配置文件的专有扩展。 这些扩展是 XML 数据片段，其中的每个片段在本机 802.11 XML 架构的 **IHV** 元素中声明。 Ihv &lt; 元素的 ihv &gt; 和 &lt; /IHV 标记中的数据 &gt; 采用 ihv 定义的格式。 **IHV** 有关本机 802.11 XML 架构的详细信息，请参阅 Microsoft Windows SDK 文档。

本节包括下列主题：

[网络配置文件概述](network-profile-overview.md)

[创建网络配置文件扩展](creating-network-profile-extensions.md)

[验证网络配置文件扩展](validating-network-profile-extensions.md)

 

 





