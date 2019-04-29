---
title: 实现文件系统，尽量减少安全威胁
description: 实现文件系统，尽量减少安全威胁
ms.assetid: a7c974ee-9f0b-4a51-aa56-5c67ee2d1180
keywords:
- 安全 WDK 文件系统、 最大程度减少威胁
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a21f793875cebe4e8c393186550760bc36702a92
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392020"
---
# <a name="implementing-file-systems-to-minimize-security-threats"></a>实现文件系统，尽量减少安全威胁


## <span id="ddk_implementing_to_minimize_security_threats_if"></span><span id="DDK_IMPLEMENTING_TO_MINIMIZE_SECURITY_THREATS_IF"></span>


会带来安全威胁的实现问题划分为一组常见的问题：

-   缓冲处理。

-   身份验证和标识。

-   访问控制。

-   处理管理。

这些问题都没有特别小说。 这些问题很知名，但这些问题重复发生在驱动程序中。 问题的一部分是大多数现有的开发工具不警告用户或防御这些类型的问题。 但是，使用明智地防御性开发技术，大多数这些问题可以消除。

本部分包括以下主题：

[缓冲区处理](buffer-handling.md)

[身份验证和标识](authentication-and-identification.md)

[访问控制](access-control.md)

[句柄管理](handle-management.md)

 

 




