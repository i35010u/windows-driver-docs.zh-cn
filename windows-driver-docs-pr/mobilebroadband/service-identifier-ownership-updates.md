---
title: 服务标识符所有权更新
description: 服务标识符所有权更新
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e82df9742abe4155b2f01df0d7c461b75142d087
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828509"
---
# <a name="service-identifier-ownership-updates"></a>服务标识符所有权更新

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]


服务标识符是在移动宽带设备中编码的一组字段， (用于 GSM 的 SIM 卡和用于 CDMA 的调制解调器) ，用于唯一标识设备。 Windows 8、Windows 8.1 和 Windows 10 使用该服务标识符下载该设备的服务元数据包。 在创建服务元数据包之前，必须向 Windows 开发人员中心硬件仪表板注册您的服务标识符。 有关注册新服务标识符的详细信息，请参阅 [创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。

根据技术，服务标识符可以包含以下内容：

-   GSM

    -   **提供程序 ID** 移动国家/地区代码和移动网络代码的组合，为5或6位数字。

    -   **提供程序名称** 预配固件时，闪存到设备上的名称。

-   CDMA

    -   **SID** CDMA 网络的系统标识符 (SID) 。

    -   **提供程序名称** 预配固件时，闪存到设备上的名称。

如果 IMSI 的所有权发生更改，则新操作员必须向发送电子邮件， sysdev@microsoft.com 其中包含以下信息：

-   操作员在 Windows 开发人员中心硬件仪表板注册过程中使用的组织名称

-   拥有 IMSI 的旧移动运营商的名称

-   受所有权更改影响的 GSM 提供程序 Id 的列表

你应收到一封确认电子邮件，其中包含你的请求收到的24小时。 不过，处理请求最多可能需要5个工作日。 如果有冲突，我们将向你发送一封电子邮件，要求提供更多信息。

 

 





