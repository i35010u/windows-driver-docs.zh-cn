---
title: 网络配置文件概述
description: 网络配置文件概述
keywords:
- 网络配置文件 WDK 本机 802.11 IHV 扩展 DLL，关于网络配置文件
- XML 片段 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea96b8c9bd11584aa036cde4dd30767f1ff04977
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834375"
---
# <a name="network-profile-overview"></a>网络配置文件概述




 

网络配置文件定义与基本服务集连接的属性， (BSS) 网络。 网络配置文件包含 XML 数据片段。 对于 Windows Vista，网络配置文件包含以下 XML 片段。

<a href="" id="profile-name--required-"></a>**配置文件名称 (必需)**  
网络配置文件的名称，它是 BSS 网络)  (SSID 的服务集标识符。

<a href="" id="standard-802-11-connectivity-settings--required-"></a>**标准802.11 连接设置 (必需)**  
此 XML 片段包含用于网络连接的标准802.11 设置，例如 BSS 网络类型 (基础结构或无线 LAN 的独立) 或类型 (WLAN) 安全性。 操作系统处理标准连接设置，并配置无线 WLAN 适配器。

<a href="" id="ihv-connectivity-extensions--optional-"></a>**IHV 连接扩展 (可选)**  
此 XML 片段包含由 IHV 定义的网络连接扩展。 操作系统将连接扩展传递到 IHV 扩展 DLL 进行处理。 DLL 负责配置 WLAN 适配器的专有扩展插件。

<a href="" id="standard-802-11-security-settings--optional-"></a>**标准802.11 安全设置 (可选)**  
此 XML 片段包含标准802.11 身份验证和密码设置，例如在 BSS 网络连接上使用的身份验证和密码算法的类型。 操作系统处理标准安全设置并配置 WLAN 适配器。

<a href="" id="ihv-security-extensions--optional-"></a>**IHV 安全扩展 (可选)**  
此 XML 片段包含由 IHV 定义的网络安全扩展。 IHV 扩展可以指定以下项之一：

-   标准安全设置。

    对于由 IHV 扩展 DLL 管理的 WLAN 适配器，DLL 负责安全算法，如 ( [RSNA](/previous-versions/windows/hardware/wireless/rsna-overview)) authentication 算法或 [AES-ccmp 报头](/previous-versions/windows/hardware/wireless/aes-ccmp) 密码算法的强大安全网络关联。 操作系统不再负责。 在这种情况下，IHV 扩展 DLL 既可以处理算法，也可以提供用于将处理卸载到 WLAN 适配器的专有方法。

-   专用安全设置。

    IHV 扩展 DLL 可提供对操作系统不支持的安全算法（如非标准或专有算法）的支持。 DLL 负责处理算法或提供用于将处理卸载到 WLAN 适配器的专有方法。

有关本机 802.11 XML 架构的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 
