---
title: 网络配置文件管理
description: 网络配置文件管理
ms.assetid: 8f430502-e436-40c2-a993-c4f1e737076a
keywords:
- IHV 扩展 DLL WDK 本机 802.11，网络配置文件
- 网络配置文件 WDK 本机 802.11 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK 网络配置文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecb175950ca3b8dcd10df8f673b3884f8e9a40ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525681"
---
# <a name="network-profile-management"></a>网络配置文件管理




 

本部分介绍管理和处理的网络配置文件由 IHV 扩展 DLL。 网络配置文件定义基本服务 (BSS) 网络连接操作的属性。

IHV 扩展 DLL 负责验证或创建到网络配置文件的专有扩展插件。 这些扩展是数据，处理的 XML 片段中声明的每个片段**IHV**本机 802.11 XML 架构元素。 中的数据&lt;IHV&gt;并&lt;/IHV&gt;标记**IHV**元素处于 IHV 定义的格式。 有关本机 802.11 XML 架构的详细信息，请参阅 Microsoft Windows SDK 文档。

本部分包括以下主题：

[网络配置文件概述](network-profile-overview.md)

[创建网络配置文件扩展](creating-network-profile-extensions.md)

[验证网络配置文件扩展](validating-network-profile-extensions.md)

 

 





