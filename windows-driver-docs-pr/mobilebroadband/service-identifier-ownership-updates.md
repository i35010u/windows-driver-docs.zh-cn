---
title: 服务标识符所有权更新
description: 服务标识符所有权更新
ms.assetid: 6cb03631-def6-44d4-a73a-0e6124e3b1f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaf44eb94498aba5efd2957c133d9db84073a015
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556130"
---
# <a name="service-identifier-ownership-updates"></a>服务标识符所有权更新

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]


服务标识符是一组字段，以移动宽带设备 （GSM 的 SIM 卡） 和 CDMA 的调制解调器进行编码，并用于唯一标识设备。 服务标识符由 Windows 8、 Windows 8.1 和 Windows 10 使用，若要下载该设备的服务元数据包。 在创建你的服务元数据包之前，必须将服务标识符注册为 Windows 开发人员中心硬件仪表板。 注册新的服务标识符的信息，请参阅[用于创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。

具体取决于技术，服务标识符可以包含以下：

-   GSM

    -   **提供程序 ID**移动国家/地区代码和移动电话网络代码，是一个 5 或 6 位数字的组合。

    -   **提供程序名称**固件预配时，该名称已刷新到设备。

-   CDMA

    -   **SID**系统标识符 (SID) 的 CDMA 网络。

    -   **提供程序名称**固件预配时，该名称已刷新到设备。

如果 IMSI 所有权发生更改，新的运算符必须发送到一封电子邮件sysdev@microsoft.com使用以下信息：

-   在 Windows 开发人员中心硬件仪表板注册过程中，运算符所使用的组织名称

-   拥有 IMSI 旧移动运营商的名称

-   GSM 所有权更改影响的提供程序 Id 的列表

应会收到确认电子邮件的 24 小时内收到你的请求。 但是，可能需要最多 5 个工作日来处理该请求。 如果我们有冲突，我们将向你发送一封电子邮件，要求其他信息。

 

 





