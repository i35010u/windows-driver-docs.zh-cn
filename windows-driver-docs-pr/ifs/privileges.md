---
title: 管理文件系统中的权限
description: 描述如何在文件系统中管理权限
keywords:
- 安全 WDK 文件系统，特权
- 权限 WDK 文件系统
- 操作特权 WDK 文件系统
- SeBackupPrivilege
- SeRestorePrivilege
- SeChangeNotifyPrivilege
- SeManageVolumePrivilege
- 卷级别管理特权 WDK 文件系统
- 遍历适当权限 WDK 文件系统
- 备份特权 WDK 文件系统
- 还原特权 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bda03d28e40b29ae5c847bbffcd23d477ef45226
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836439"
---
# <a name="managing-privileges-in-a-file-system"></a>管理文件系统中的权限

权限是一个完全独立的机制，操作系统使用它来控制特定操作。 如果调用方持有和启用了特权，则每个特权都与特定的操作相关联。 请注意以下两种情况：

- 权限必须由调用方持有。

- 还必须启用特权。

此处所述的原则称为最小特权，要求在使用权限之前启用权限，而不是只是假设，以最大程度地减少用户可能会因疏忽而执行的操作。 例如， **SeRestorePrivilege** 通常允许调用方绕过常用检查来对文件进行写访问。 在复制文件时，管理员可能不希望实际重写常规安全检查，但在使用备份/还原实用程序还原同一文件时需要这样做。

对于文件系统，有很多特权通常用于修改正常行为 (特别要注意的是，系统) 安全检查。 这些权限包括：

- **SeBackupPrivilege** 允许文件内容检索，即使文件的安全描述符可能不会授予此类访问权限。 启用了 **SeBackupPrivilege** 的调用方免去需要进行基于 ACL 的任何安全检查。

- **SeRestorePrivilege** 允许对文件内容进行修改，即使文件的安全描述符可能不会授予此类访问权限。 此函数还可用于更改所有者和保护。

- **SeChangeNotifyPrivilege** 允许直接遍历。 此特权是 Windows 中的一项重要优化，因为在路径中的每个目录上执行安全检查所需的成本都是面对的。

- **SeManageVolumePrivilege** 允许在 Windows XP 和更高版本上进行特定的卷级别管理操作，例如锁量、碎片整理、卷卸除以及设置有效的数据长度。 请注意，此特定权限由文件系统驱动程序基于 FSCTL 操作显式强制执行。 在这种情况下，文件系统做出策略决定来强制实施此权限。 确定此特权是否由安全引用监视器控制，作为正常权限检查的一部分。

虽然有许多其他权限，但它们对于文件系统通常是不透明的，因此仅由安全引用监视器来解释。

用于管理文件系统中权限的关键 Windows 例程包括：

- [**SePrivilegeCheck**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seprivilegecheck)-此例程用于检查一组特定权限。

- [**SeSinglePrivilegeCheck**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-sesingleprivilegecheck)-此例程执行单个特定权限的检查，它是 [**SePrivilegeCheck**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seprivilegecheck)的优化版本。

- [**SeAccessCheck**](/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)--此例程对某个对象执行正常的访问检查， (通常是) 文件系统的文件对象。

- [**SeFreePrivileges**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-sefreeprivileges)--此例程释放先前对 [**SeAccessCheck**](/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)的调用返回的特权块。

- [**SeAppendPrivileges**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seappendprivileges)--此例程将已启用的特权添加到 ACCESS_STATE 结构。 通常，文件系统会在 IRP_MJ_CREATE 处理期间使用传递给它的 ACCESS_STATE。
