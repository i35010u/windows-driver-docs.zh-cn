---
title: 访问控制列表
description: 访问控制列表
keywords:
- 安全描述符 WDK 文件系统，访问控制列表
- 描述符文件系统、访问控制列表
- 访问控制列表 WDK 文件系统
- ACL WDK 文件系统
- 随机 ACL WDK 文件系统
- 系统 ACL WDK 文件系统
- 强制控制 WDK 文件系统
- 受保护对象 WDK 文件系统
- 对象安全性 WDK 文件系统
- 访问控制入口 WDK 文件系统
- ACE WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dbf91a27faf163bd1078688cea7aa19308f5ec2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839555"
---
# <a name="access-control-list"></a>访问控制列表


## <span id="ddk_access_control_list_if"></span><span id="DDK_ACCESS_CONTROL_LIST_IF"></span>


 (ACL) 的访问控制列表是操作系统创建的一系列 Ace，用来控制与某种特定 (保护的) 对象关联的安全行为。 在 Windows 中有两种类型的 Acl：

-   **自由 ACL**-这是一个零个或多个 ace 的列表，用于描述受保护对象的访问权限。 它是自由的，因为所授予的访问权限是所有者或任何具有相应权限的用户。

-   **系统 ACL**-这是一个零个或多个用于描述受保护对象的审核和警报策略的 ace 的列表。

术语 "自由" 指强制控制和随机控制之间的差异。 在使用强制控制的环境中，对象的所有者可能不能授予对该对象的访问权限。 在任意环境（例如 Windows）中，允许对象的所有者授予此类访问权限。 强制控制通常与非常严格的安全环境（例如，使用事关 security 的环境）相关联，其中系统必须阻止在同一系统上的用户之间泄漏敏感信息。

构造 ACL 的驱动程序将遵循几个关键步骤：

1.  为 ACL 分配存储空间。

2.  初始化 ACL。

3.  向 ACL 添加零个 (或多个) Ace。

下面的代码示例演示如何构造 ACL：

```cpp
    dacl = ExAllocatePool(PagedPool, PAGE_SIZE);
    if (!dacl) {
        return;
    }
    status = RtlCreateAcl(dacl, PAGE_SIZE, ACL_REVISION);
    if (!NT_SUCCESS(status)) {
        ExFreePool(dacl);
        return;
    }
```

前面的代码段创建了一个空 ACL。 此代码示例分配了大量内存，因为我们不知道 ACL 所需的大小。

此时，ACL 为空，因为它没有 ACE 条目。 空 ACL 将拒绝对任何尝试访问对象的用户的访问，因为没有可授予此类访问权限的条目。 下面的代码段向此 ACL 添加 ACE：

```cpp
    status = RtlAddAccessAllowedAce(dacl, ACL_REVISION,  FILE_ALL_ACCESS, SeExports->SeWorldSid);
    if (!NT_SUCCESS(status)) {
        ExFreePool(dacl);
        return;
    }
```

此项现在将授予对访问对象的任何实体的访问权限。 这是世界访问 SID (SeWorldSid) 的目的，通常在其他 Windows 系统实用工具中以 "Everyone" 的形式表示。

请注意，在构造 Acl 时，必须将访问权限拒绝的 ACE 条目排序到 ACL 的开头，然后访问 ACL 末尾的允许 ACE 条目。 这是因为当安全引用监视器执行了对 ACL 的评估时，它会在找到拒绝的 Ace 之前，授予访问权限。 此行为在 Microsoft Windows SDK 中进行了很好的记录，但它与安全引用监视器用来确定是否应授予或拒绝访问权限的特定机制相关。

 

 




