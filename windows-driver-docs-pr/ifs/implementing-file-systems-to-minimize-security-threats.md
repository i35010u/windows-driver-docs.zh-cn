---
title: 实现文件系统，尽量减少安全威胁
description: 实现文件系统，尽量减少安全威胁
keywords:
- 安全 WDK 文件系统，最大限度地减少威胁
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81f74f680881d286e64b7199c22421e23bffc342
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783259"
---
# <a name="implementing-file-systems-to-minimize-security-threats"></a>实现文件系统，尽量减少安全威胁


## <span id="ddk_implementing_to_minimize_security_threats_if"></span><span id="DDK_IMPLEMENTING_TO_MINIMIZE_SECURITY_THREATS_IF"></span>


构成安全威胁的实现问题属于一组常见问题：

-   缓冲区处理。

-   身份验证和标识。

-   访问控制。

-   处理管理。

这些问题都不是特别 novel。 这些问题众所周知，但驱动程序出现这些问题。 问题的一部分是大多数现有开发工具不会警告用户或缓解这些类型的问题。 但是，使用明智的防御性开发技术，可以消除其中的大多数问题。

本节包括下列主题：

[缓冲区处理](buffer-handling.md)

[身份验证和标识](authentication-and-identification.md)

[访问控制](access-control.md)

[处理管理](handle-management.md)

 

 




