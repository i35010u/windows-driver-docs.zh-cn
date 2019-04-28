---
title: 网络配置文件概述
description: 网络配置文件概述
ms.assetid: b7d902db-4918-4e9f-a7e0-3bb6c5ed1dfb
keywords:
- 网络配置文件 WDK 本机 802.11 IHV 扩展 DLL，有关网络配置文件
- XML 片段 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 999a7f743f3ee842b649840420c3caec99a97d04
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331853"
---
# <a name="network-profile-overview"></a>网络配置文件概述




 

网络配置文件定义基本的服务集 (BSS) 网络连接的属性。 网络配置文件包含 XML 数据片段。 适用于 Windows Vista 网络配置文件包含以下 XML 片段。

<a href="" id="profile-name--required-"></a>**配置文件名称 （必需）**  
网络配置文件，这是服务的名称设置标识符 (SSID) 的 BSS 网络。

<a href="" id="standard-802-11-connectivity-settings--required-"></a>**标准 802.11 连接设置 （必需）**  
此 XML 片段包括标准 802.11 网络连接，如 BSS 网络类型 （基础结构或独立） 或类型的无线 LAN (WLAN) 安全设置。 操作系统处理的标准连接设置，并使用它们来配置无线 WLAN 适配器。

<a href="" id="ihv-connectivity-extensions--optional-"></a>**IHV 连接扩展 （可选）**  
下面的 XML 片段包含，由 IHV 定义的网络连接的扩展。 操作系统将连接扩展传递给 IHV 扩展 DLL 中进行处理。 DLL 负责 WLAN 适配器配置为具有专有扩展插件。

<a href="" id="standard-802-11-security-settings--optional-"></a>**标准 802.11 安全设置 （可选）**  
此 XML 片段包括标准的 802.11 网络连接的身份验证和密码设置，例如要在 BSS 上使用的身份验证和加密算法的类型。 操作系统处理的标准安全设置，并使用它们来配置 WLAN 适配器。

<a href="" id="ihv-security-extensions--optional-"></a>**IHV 安全扩展插件 （可选）**  
下面的 XML 片段包含网络安全规定的 IHV 的扩展。 IHV 扩展可以指定以下值之一：

-   标准安全设置。

    对于由 IHV 扩展 DLL 将 WLAN 适配器，该 DLL 负责安全算法，例如可靠的安全网络关联 ( [RSNA](https://docs.microsoft.com/windows-hardware/drivers/network/rsna-overview)) 身份验证算法或[AES CCMP](https://docs.microsoft.com/windows-hardware/drivers/network/aes-ccmp)密码算法。 操作系统不再负责。 在此情况下，IHV 扩展 DLL 可以处理算法，或者提供用于卸载到 WLAN 适配器处理的专有方法。

-   专用安全设置。

    不支持的操作系统，如非标准或专有算法的安全算法，IHV 扩展 DLL 可以提供支持。 DLL 负责处理算法，或提供用于卸载到 WLAN 适配器处理的专有方法。

有关本机 802.11 XML 架构的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 





