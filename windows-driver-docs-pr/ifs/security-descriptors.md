---
title: 安全描述符
description: 安全描述符
ms.assetid: 4c3200a8-63f4-4398-aed1-b90150027829
keywords:
- 安全 WDK 文件系统、 描述符
- 安全描述符 WDK 文件系统
- 描述符 WDK 文件系统
- 安全描述符 WDK 文件系统，有关安全描述符
- 描述符 WDK 文件系统，有关安全描述符
- 存储 WDK 文件系统
- 脱机的安全描述符存储 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f81bc7d5d53a30126ca9a698c50aa5dfdd9b2ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563377"
---
# <a name="security-descriptors"></a>安全描述符


## <span id="ddk_security_descriptors_if"></span><span id="DDK_SECURITY_DESCRIPTORS_IF"></span>


Windows 文件系统可能支持的存储和管理与文件系统中的单个存储单元相关联的安全描述符。 安全控件的粒度级为完全取决于文件系统。 例如，一个文件系统可能会维护包含给定的存储卷上的所有内容，而另一个可能会提供覆盖某一特定文件的不同部分的安全描述符的单独的安全描述符。 大多数开发人员将与合适的模型是所提供的现有 Windows 文件系统：

-   NTFS-支持的每个文件 （或目录） 的安全描述符模型。 NTFS 是有效的安全描述符，其存储中存储单个副本的每个安全描述符，即使它由许多不同的文件。

-   FAT CDFS，UDF，不支持安全描述符。

-   RDBSS 和 SMB 网络重定向程序 — 提供类似于所提供的远程卷的支持。

但是，这些文件系统中，不表示文件系统的 Windows 安全的所有可能的实现。

Windows 安全描述符包含的四个不同部分：

-   对象的所有者安全标识符 (SID)。 对象的所有者始终具有重置对象上的安全功能。 这是确保，例如，所有对象的访问权限可以都删除的好办法。 因为即使所有者删除其执行所有操作的能力，此固有权限允许它们以还原对对象及其安全权限。

-   对象的默认组可选的安全标识符 (SID)。 组所有权的概念是指不需要在 Windows，但对于某些应用程序很有用。

-   系统访问控制列表 (SACL) 描述的安全描述符的审核策略。

-   自由访问控制列表 (DACL) 描述的安全描述符的访问策略。

下图说明了 windows 安全描述符。

![说明 windows 安全描述符的关系图](images/fssecurity-01.png)

安全描述符是可变的对象，以及与每个单独的子组件正在变量的大小。 为了便于进行脱机存储的安全描述符，安全描述符可能采用自相关格式，在其中用例标头为中的安全描述符的特定组件的缓冲区的偏移量。 内存中格式包含的各个部分的安全描述符的指针值。 对于文件系统中，自相关格式是通常最有用，因为它允许使用简单存储和检索从持久性存储区的安全描述符。 生成安全描述符的应用程序是更有可能使用的内存中的格式。 安全引用监视器提供转换例程以从一种格式转换为其他。

本部分包括以下主题：

[安全标识符](security-identifier.md)

[Access Mask](access-mask.md)

[访问控制项](access-control-entry.md)

[访问控制列表](access-control-list.md)

 

 




