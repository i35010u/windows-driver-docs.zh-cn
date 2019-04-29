---
title: 什么是驱动程序安全性
description: 什么是驱动程序安全性
ms.assetid: df959e2b-c779-4171-b408-32fbe52ed7af
keywords:
- 安全 WDK 文件系统、 文件系统安全性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e5bdb9ce1ab651bcf6a9b73769d1fbd5dccf3a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322222"
---
# <a name="what-is-driver-security"></a>什么是驱动程序安全性


## <span id="ddk_what_is_driver_security_if"></span><span id="DDK_WHAT_IS_DRIVER_SECURITY_IF"></span>


相对于驱动程序，任何用户可以执行的操作，导致出现故障的方式，它会导致系统崩溃或变得不可用的驱动程序是安全漏洞。 大多数开发人员工作时在其驱动程序，其重点是获取驱动程序才能正常工作，还是恶意入侵者将尝试进行攻击系统中的漏洞。 这是文件系统和文件系统筛选器驱动程序，它是一些最复杂类型的驱动程序编写的更多案例。

但是，在产品版本之后, 有用户尝试探测并识别安全漏洞。 因此，它适合开发人员能够在设计和实施阶段请考虑以下问题，以便这类漏洞存在的可能性降至最低。 目标是产品的尽可能消除同样多的安全问题发生前已发布的一部分。

实现安全驱动程序需要的设计器 （有意识地思考的驱动程序的潜在威胁）、 实施者 （采用防御方式进行编码可攻击的源的常见操作） 和 （主动尝试测试团队的协作查找攻击）。 通过正确地协调所有这些活动，将大大增强的驱动程序的安全性。

 

 




