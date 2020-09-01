---
title: 文件系统中的安全描述符
description: 描述安全描述符的文件系统支持
ms.assetid: 4c3200a8-63f4-4398-aed1-b90150027829
keywords:
- 安全 WDK 文件系统、描述符
- 安全描述符 WDK 文件系统
- 描述符文件系统
- 安全描述符 WDK 文件系统，关于安全描述符
- 描述符文件系统，关于安全描述符
- 存储 WDK 文件系统
- 脱机安全描述符存储 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b667db4fb22f71c36ce7972d76e63c6e1d168fc5
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067362"
---
# <a name="security-descriptors-in-file-systems"></a>文件系统中的安全描述符

Windows 文件系统可能支持存储和管理与文件系统中的单个存储单元关联的 [安全描述符](../kernel/security-descriptors.md) 。 安全控制的粒度完全取决于文件系统。 例如，一个文件系统可能会维护一个安全描述符，其中包含给定存储卷上的所有内容，而另一个则可能提供涵盖单个给定文件的不同部分的安全描述符。 大多数开发人员都熟悉的模型是现有 Windows 文件系统提供的模型：

- NTFS 支持每个文件 (或目录) 安全描述符模型。 NTFS 在其安全描述符存储中有效，只存储每个安全描述符的单个副本，即使它被许多不同的文件使用。

- FAT、CDFS、UDF 不支持安全描述符。

- RDBSS 和 SMB 网络重定向器提供的支持与远程卷提供的支持相同。

但这些文件系统并不表示文件系统的 Windows 安全的所有可能实现。

Windows 安全描述符由四个不同的部分组成：

- 对象所有者 (SID) 的安全标识符。 对象的所有者始终能够重置对象的安全性。 这是一种很好的方法，可确保可以删除对对象的所有访问。 由于所有者删除了其执行所有操作的能力，因此，这种固有的权限允许他们还原对对象的安全权限。

- 可选的安全标识符 (对象的默认组的 SID) 。 组所有权的概念是 Windows 中不需要的，但对于某些应用程序很有用。

- 系统访问控制列表 (SACL) ，描述安全描述符的审核策略。

-  (DACL) 的自由访问控制列表，该列表描述安全描述符的访问策略。

下图说明了一个 windows 安全描述符。

![阐释 windows 安全描述符的关系图](images/fssecurity-01.png)

安全描述符是大小可变的对象，其中的每个子组件也都是可变的。 为了便于脱机存储安全描述符，安全描述符可以是自相关格式，在这种情况下，标头是缓冲区内到安全描述符的特定部分的偏移量。 内存中的格式由指向安全说明符各个部分的指针值组成。 对于文件系统，自相关格式通常最有用，因为它允许简单存储和从持久存储中检索安全描述符。 构建安全描述符的应用程序更有可能使用内存中的格式。 安全参考监视器提供转换例程，以将其从一种格式转换为另一种格式。

本节包括下列主题：

[安全标识符](security-identifier.md)

[访问掩码](access-mask.md)

[访问控制项](access-control-entry.md)

[访问控制列表](access-control-list.md)