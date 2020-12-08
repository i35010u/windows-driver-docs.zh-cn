---
title: 安全威胁模型
description: 安全威胁模型
keywords:
- 安全 WDK 文件系统，威胁模型
- 系统威胁模型 WDK 文件系统
- 安全威胁模型 WDK 文件系统
- 安全威胁模型的有关 WDK 文件系统的威胁模型
- 安全威胁模型 WDK 文件系统，关于安全威胁模型
- 攻击 WDK 安全性
- I/o WDK 安全性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2052b1eb8e86657f3ba1b31ef20a616d449b1b3b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823263"
---
# <a name="security-threat-models"></a>安全威胁模型


## <span id="ddk_designing_with_security_threat_models_if"></span><span id="DDK_DESIGNING_WITH_SECURITY_THREAT_MODELS_IF"></span>


考虑到安全性，一种常见的方法是创建具体的威胁模型，以尝试描述可能的攻击类型。 此方法在设计文件系统或文件系统筛选器驱动程序时很有用，因为它会强制开发人员考虑针对驱动程序的潜在攻击媒介。 如果已确定潜在的威胁，驱动程序开发人员就可以考虑防御这些威胁，从而加强驱动程序组件的总体安全性。

考虑安全威胁模型时，区分 "操作驱动程序管理" 的操作将代表用户 i/o 请求，这一点也很重要 (这些请求受安全检查) 和驱动程序本身启动的 i/o 操作 (默认情况下不受安全检查) 。 对于一个驱动程序的用户模式请求，还可以通过内部 FSCTL 或 IOCTL 请求（ (Srv.sys 驱动程序）传递给另一驱动程序，如) ，进一步使这些问题更加复杂。

对于内核模式驱动程序的开发人员，应考虑以下重要问题：

-   驱动程序启动的 i/o 操作会绕过本地系统的安全检查

-   驱动程序启动的 i/o 操作绕过大多数参数验证检查。

-   驱动程序是受信任计算基础的一部分，因此可以控制整个系统。

例如，假设有一个能够在系统上成功加载驱动程序的恶意程序。 这会为其提供极大的控制，基本上会损害系统。 如果应用程序可以利用驱动程序的一项功能来实现同样的功能，则可以将控制权移交给应用程序并将系统泄露。

在考虑安全时，Microsoft 使用 "STRIDE" 模型：

-   S--[欺骗标识](spoofing-identity.md)。

-   T--[篡改数据](tampering-with-data.md)。

-   R--[抵赖](repudiation.md)。

-   I--[信息泄漏](information-disclosure.md)。

-   D--[拒绝服务](denial-of-service.md)。

-   电子--[特权提升](elevation-of-privilege.md)。

此处的基本原则标识了可能发生的特定类型的系统泄露。 其中的一些原则通常是对驱动程序的有效性，但都具有文件系统和文件系统筛选器驱动程序的有效性。

 

 




