---
title: 什么是驱动程序安全性
description: 什么是驱动程序安全性
keywords:
- 安全 WDK 文件系统，关于文件系统安全
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e7e6762c48dc8db7796085b46fc60ece4ad5da1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820275"
---
# <a name="what-is-driver-security"></a>什么是驱动程序安全性


## <span id="ddk_what_is_driver_security_if"></span><span id="DDK_WHAT_IS_DRIVER_SECURITY_IF"></span>


对于驱动程序，用户可以执行的任何操作都会导致驱动程序出现故障，使系统崩溃或变得不可用是一个安全缺陷。 当大多数开发人员都在使用其驱动程序时，其重点是使驱动程序正常工作，而不是恶意入侵者是否会尝试利用系统中的漏洞。 对于文件系统和文件系统筛选器驱动程序，这种情况更是一种情况，这是一些最复杂的驱动程序类型。

但是，在产品发布后，用户可以尝试探测并识别安全漏洞。 因此，开发人员可以在设计和实施阶段考虑这些问题，以最大程度地减少此类洞存在的可能性。 目标是在已发布产品的一部分之前消除尽可能多的安全漏洞。

实现安全驱动程序需要 (特意考虑到对驱动程序) 的潜在威胁，实施人员 (保守编码常见操作，这些操作可能是攻击的来源) ，测试团队 (主动尝试查找攻击) 。 通过适当地协调所有这些活动，驱动程序的安全性将大大增强。

 

 




