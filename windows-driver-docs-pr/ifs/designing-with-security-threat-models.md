---
title: 使用安全威胁模型进行设计
description: 使用安全威胁模型进行设计
ms.assetid: a505df1a-82c0-4e0b-88bb-d96654a098fb
keywords:
- 安全 WDK 文件系统，威胁模型
- 威胁模型 WDK 的文件系统
- 安全威胁模型 WDK 的文件系统
- 威胁建模 WDK 文件系统，以了解安全威胁模型
- 安全威胁模型 WDK 文件系统，以了解安全威胁模型
- 攻击 WDK 安全
- I/O WDK 安全
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c90a12159c0d97f87ef1e4f036020e35668dd9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521991"
---
# <a name="designing-with-security-threat-models"></a>使用安全威胁模型进行设计


## <span id="ddk_designing_with_security_threat_models_if"></span><span id="DDK_DESIGNING_WITH_SECURITY_THREAT_MODELS_IF"></span>


出于安全考虑，常见的方法是创建会描述的是可能的攻击类型的特定威胁模型。 设计文件系统或文件系统筛选器驱动程序，因为它会强制开发人员需要考虑潜在的攻击媒介，针对一个驱动程序时，此方法很有用。 确定潜在威胁后，驱动程序开发人员则可以考虑防御这些威胁，从而有助于巩固理解驱动程序组件的总体安全性的方式。

在考虑安全威胁模型时，也很重要的驱动程序代表用户 I/O 请求 （它们受到安全检查） 管理的操作和由驱动程序本身 （这不是默认情况下启动的 I/O 操作之间进行区分受安全检查）。 用户模式下向一个请求，驱动程序可能还传递到另一个驱动程序通过内部 FSCTL 或 IOCTL 请求 （Srv.sys 驱动程序，例如），进一步使问题变得复杂。

对于开发人员的内核模式驱动程序，应考虑下列重要问题：

-   由驱动程序启动的 I/O 操作绕过本地系统上的安全检查

-   由驱动程序启动的 I/O 操作绕过大多数参数验证检查。

-   驱动程序是受信任计算库的一部分，因此可以控制整个系统。

例如，假设可以成功加载的驱动程序在系统上的恶意程序。 这将为其提供极大的控制，并将实质上是危害系统。 如果应用程序可以利用您的驱动程序来实现相同目的的一项功能，您可以移交到应用程序的控制并破坏系统。

在考虑安全时，Microsoft 将使用"STRIDE"模型：

-   S-[身份欺骗](spoofing-identity.md)。

-   T-[篡改数据](tampering-with-data.md)。

-   R-[否认](repudiation.md)。

-   我-[信息泄露](information-disclosure.md)。

-   D-[拒绝服务](denial-of-service.md)。

-   E-[提升权限](elevation-of-privilege.md)。

此处的基本原理标识特定类型的可能发生的系统受到损害。 这些原则的一些一般情况下，有驱动程序的有效性，但是都具有对文件系统和文件系统筛选器驱动程序的有效性。

 

 




