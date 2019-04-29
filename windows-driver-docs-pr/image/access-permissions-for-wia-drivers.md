---
title: WIA 驱动程序的访问权限
description: WIA 驱动程序的访问权限
ms.assetid: 593e9367-5304-4b04-8597-4a7c498b9f47
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4e7358e254013db4b48becc17d9bf83359ee9135
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377634"
---
# <a name="access-permissions-for-wia-drivers"></a>WIA 驱动程序的访问权限

为了使用相同的命名的对象驱动程序和另一个组件，正确的权限应设置为该对象在创建时。 通常情况下，这涉及到在该对象的安全描述符中设置适当的 DACL。

执行此操作的简单办法是使用安全描述符定义语言 (SDDL) 函数。 SDDL 代表是简单的字符串表示形式的 Windows 安全描述符或 SD. 一个 SDDL 字符串可以转换为 SD 和 SDs 可以转换为可用于比较两个安全描述符的 SDDL 字符串。

有关使用 SDDL 设置上一个事件对象的访问权限的示例，请参阅[WIA 安全和安全描述符](wia-security-and-security-descriptors.md)。

