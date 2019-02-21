---
title: 权限
description: 权限
ms.assetid: a8df1a44-6fb7-4c16-a29d-785d06dd50e4
keywords:
- 安全 WDK 文件系统权限
- WDK 的文件系统权限
- 操作的权限 WDK 的文件系统
- SeBackupPrivilege
- SeRestorePrivilege
- SeChangeNotifyPrivilege
- SeManageVolumePrivilege
- 卷级管理特权 WDK 的文件系统
- 遍历正确权限 WDK 的文件系统
- 备份特权 WDK 文件系统
- 还原权限 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e39a8149f75a1de93d7f05854961196d9a87baa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541487"
---
# <a name="privileges"></a>权限


## <span id="ddk_privileges_if"></span><span id="DDK_PRIVILEGES_IF"></span>


权限是由操作系统用来控制特定操作的完全独立机制。 每个权限都有与其关联如果特权保存，并启用由调用方可能执行的特定操作。 请注意两个条件：

-   必须由调用方具有的权限。

-   此外必须启用特权。

下面的原则，称为最小特权，需要的权限被启用之前使用它们而不是只需假定，若要最大程度减少用户可能无意中执行它们意料之外的操作的机会。 例如， **SeRestorePrivilege**通常情况下会允许调用方以绕过的常用文件的写入访问权限检查。 管理员可能不想要复制文件时实际上重写常规安全检查，但会想要执行此操作时还原该文件使用备份/还原实用程序。

对于文件系统，有数通常用于修改系统的正常行为 （值得注意的是，安全检查） 的权限。 这些权限是：

-   **SeBackupPrivilege**-允许文件内容检索，即使该文件上的安全描述符可能会授予此类的访问权限。 与调用方**SeBackupPrivilege**启用项目无需任何基于 ACL 的安全检查。

-   **SeRestorePrivilege**-允许文件内容修改，即使该文件上的安全描述符可能会授予此类的访问权限。 此函数还可用于更改所有者和保护。

-   **SeChangeNotifyPrivilege**-允许遍历权限。 此权限是在 Windows 中，重要的优化，因为持有此特权通过排除路径中执行对每个单个目录的安全检查的成本。

-   **SeManageVolumePrivilege**-允许特定的卷级管理操作，如锁定卷、 碎片整理、 卷卸除，和 Windows XP 及更高版本的有效的数据长度设置。 请注意此特定权限显式由主要基于 FSCTL 操作的文件系统驱动程序强制执行。 在这种情况下，文件系统可以强制执行此权限的策略决策。 确定调用方是否具有此权限是通过安全引用监视器作为正常权限检查的一部分。

虽然有许多其他权限，它们是通常情况下不透明的文件系统，因此只能解释安全引用监视器。

用于管理文件系统中的特权的关键 Windows 例程是：

-   [**SePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff556686)-此例程执行检查的一组特定的必要权限。

-   [**SeSinglePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563740)-此例程单一的特定权限时进行检查; 的优化的版本[ **SePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff556686)。

-   [**SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)-此例程执行普通访问检查的对象 （通常情况下的文件系统的文件对象）。

-   [**SeFreePrivileges**](https://msdn.microsoft.com/library/windows/hardware/ff556656)-此例程将释放通过以前调用返回的特权块[ **SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)。

-   [**SeAppendPrivileges**](https://msdn.microsoft.com/library/windows/hardware/ff554762)-此例程将已启用的权限添加到所需的访问\_状态结构。 通常情况下，文件系统将使用的访问权限\_期间 IRP 传递给它的状态\_MJ\_创建处理。

 

 




