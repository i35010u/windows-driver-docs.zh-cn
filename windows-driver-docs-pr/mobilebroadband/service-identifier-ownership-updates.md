---
title: 服务标识符所有权更新
description: 服务标识符所有权更新
ms.assetid: 6cb03631-def6-44d4-a73a-0e6124e3b1f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaf44eb94498aba5efd2957c133d9db84073a015
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323703"
---
# <a name="service-identifier-ownership-updates"></a>服务标识符所有权更新

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]


服务标识符是在移动宽带设备（用于 GSM 的 SIM 卡和用于 CDMA 的调制解调器）中编码的一组字段，用于唯一标识设备。 Windows 8、Windows 8.1 和 Windows 10 使用该服务标识符下载该设备的服务元数据包。 在创建服务元数据包之前，必须向 Windows 开发人员中心硬件仪表板注册您的服务标识符。 有关注册新服务标识符的详细信息，请参阅[创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。

根据技术，服务标识符可以包含以下内容：

-   GSM

    -   **提供程序 ID**移动国家/地区代码和移动网络代码的组合，为5或6位数字。

    -   **提供程序名称**预配固件时，闪存到设备上的名称。

-   CDMA

    -   **SID**CDMA 网络的系统标识符（SID）。

    -   **提供程序名称**预配固件时，闪存到设备上的名称。

如果 IMSI 的所有权发生更改，则新操作员必须发送一封电子邮件到 sysdev@microsoft.com，其中包含以下信息：

-   操作员在 Windows 开发人员中心硬件仪表板注册过程中使用的组织名称

-   拥有 IMSI 的旧移动运营商的名称

-   受所有权更改影响的 GSM 提供程序 Id 的列表

你应收到一封确认电子邮件，其中包含你的请求收到的24小时。 不过，处理请求最多可能需要5个工作日。 如果有冲突，我们将向你发送一封电子邮件，要求提供更多信息。

 

 





