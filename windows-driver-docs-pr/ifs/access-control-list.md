---
title: 访问控制列表
description: 访问控制列表
ms.assetid: e682c2cc-ddd7-482b-b4f2-3e163d914752
keywords:
- 安全描述符 WDK 文件系统，访问控制列表
- 描述符 WDK 文件系统，访问控制列表
- 访问控制列表 WDK 文件系统
- ACL WDK 的文件系统
- 自由 ACL WDK 的文件系统
- 系统 ACL WDK 的文件系统
- 强制控件 WDK 文件系统
- 受保护的对象 WDK 的文件系统
- 对象安全 WDK 文件系统
- 访问控制条目 WDK 文件系统
- ACE WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7e1c83f54da0f8fce1905d078080d171078cfa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546849"
---
# <a name="access-control-list"></a>访问控制列表


## <span id="ddk_access_control_list_if"></span><span id="DDK_ACCESS_CONTROL_LIST_IF"></span>


访问控制列表 (ACL) 是一组 Ace 由操作系统创建，以控制与某种类型的给定 （受保护的） 对象关联的安全行为。 在 Windows 中有两种类型的 Acl:

-   **自由 ACL**-这是一组描述受保护对象的访问权限的零个或多个 Ace。 这是随机的因为访问权限授予是所有者或具有相应权限的任何用户的决定。

-   **系统 ACL**-这是一个列表的零个或多个 Ace 的描述的审核和警报的受保护对象的策略。

"随机"一词表示必填字段和自定义控件之间的区别。 在环境中使用必需的控件，对象的所有者可能不能授予对对象的访问。 在自定义环境中，如 Windows，对象的所有者被允许授予此类访问权限。 强制控件是通常与非常严格的安全措施环境，如那些使用化的安全性，其中系统必须防止泄露敏感信息的同一系统上的用户之间的关联。

构造一个 ACL 的驱动程序需要执行几个关键步骤：

1.  为 ACL 分配存储空间。

2.  初始化 ACL。

3.  将零个 （或更多） 的 Ace 添加到 ACL。

下面的代码示例演示如何构造 ACL:

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

上一代码片段创建一个空的 ACL。 代码示例分配大量内存，因为我们不知道 ACL 所需的大小。

此时，ACL 为空，因为它没有任何 ACE 条目。 一个空的 ACL 拒绝任何人在试图访问对象，因为没有项授予此类访问权限的访问。 下面的代码段将一个 ACE 添加到此 ACL:

```cpp
    status = RtlAddAccessAllowedAce(dacl, ACL_REVISION,  FILE_ALL_ACCESS, SeExports->SeWorldSid);
    if (!NT_SUCCESS(status)) {
        ExFreePool(dacl);
        return;
    }
```

此项现在会授予访问权限访问该对象的任何实体。 这是访问 SID (SeWorldSid)，它通常表示为"Everyone"访问其他 Windows 系统实用程序中的用途。

请注意，在构造时 Acl，它是重要的顺序访问被拒绝 ACE 的 ACL，开头的条目，然后访问允许 ACE 的 ACL 末尾的项。 这是因为安全引用监视器执行计算的 acl 时它将授予访问权限会在之前找到拒绝的 Ace 授予访问权限的 ACE。 此行为也记录在 Microsoft Windows SDK 中，但它与安全引用监视器使用来确定是否应授予或拒绝访问的特定机制。

 

 




