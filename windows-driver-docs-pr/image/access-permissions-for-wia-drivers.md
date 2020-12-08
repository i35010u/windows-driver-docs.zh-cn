---
title: WIA 驱动程序的访问权限
description: WIA 驱动程序的访问权限
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: d9e0b2d97b5fc13a7e5c629f87eeecafcc82e6ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808307"
---
# <a name="access-permissions-for-wia-drivers"></a>WIA 驱动程序的访问权限

为了使驱动程序和其他组件使用同一命名对象，应在创建该对象时为该对象设置正确的权限。 通常，这涉及到在该对象的安全描述符中设置相应的 DACL。

执行此操作的一种简单方法是使用安全描述符定义语言 (SDDL) 函数。 SDDL 代表 Windows 安全描述符或 SD 的简单字符串表示形式。 SDDL 字符串可转换为 SD，SDs 可以转换为 SDDL 字符串，这在比较两个安全描述符时非常有用。

有关使用 SDDL 设置事件对象上的访问权限的示例，请参阅 [WIA 安全和安全描述符](wia-security-and-security-descriptors.md)。

