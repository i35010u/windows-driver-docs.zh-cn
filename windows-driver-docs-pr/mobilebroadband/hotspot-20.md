---
title: 热点 2.0
description: 热点 2.0
ms.assetid: 4dbd242d-8745-4ab2-b1dc-9f9dd9a73b42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9c92ebba5faa108931b355f3b96a37593a48765
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902645"
---
# <a name="hotspot-20"></a>热点 2.0

热点2.0 是对热点进行无缝身份验证的标准。 热点2.0 提供客户端和访问点之间的加密连接。 它在建立连接之前，使用 IEEE 802.11 u 与提供程序进行通信。 使用 WPA2-Enterprise 和多种 EAP 方法之一提供身份验证和加密。

下表描述了由热点2.0 定义的常见凭据类型：

|凭据|EAP 方法|支持的 EAP 方法|用户可以输入凭据|操作员可以预配凭据|
|----|----|----|----|----|
|用户名和密码|EAP-TTLS|是|是|否|
|证书|EAP-TTLS|是|是|否|
|SIM|EAP-SIM 或 EAP-称为|是|是|是|

\*用户可以从证书中进行选择，或 SIM 已经存在于系统上。

Windows 8 和 Windows 8.1 不支持热点2.0 的发现或联机注册部分，但支持 WPA2-企业和热点2.0 规范所需的所有 EAP 方法。 因此，当用户已有凭据时，Windows 8 和 Windows 8.1 可以连接到热点2.0 网络。

由于 Windows 8 和 Windows 8.1 不支持 802.11 u 发现，因此，操作员必须预配包含其网络适用 Ssid 的无线配置文件的 Windows 8 或 Windows 8.1。

Windows 10 完全支持热点2.0 版本1，包括发现和配置文件创建。
