---
title: 更新包感知驱动程序的 INF
description: 更新包感知驱动程序的 INF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07abe2567e05644e6f5a5cd848589c54675335ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835471"
---
# <a name="updating-your-package-aware-drivers-inf"></a>更新包感知驱动程序的 INF


将核心驱动程序与包感知驱动程序捆绑在一起后，下一步是更新包感知驱动程序的 INF 文件。

包感知驱动程序的 INF 文件需要引用更新后的核心驱动程序包。 为此，请使用核心型号 GUID 标识核心驱动程序包，如 [编写核心驱动程序](writing-core-drivers.md)中所述。 除了标识核心驱动程序包之外，还需要对 INF 文件进行以下两项更改。

首先，指定核心驱动程序可接受的最低版本，以便仅使用更新的版本。 指定最小版本后，可以避免使用较旧的、不兼容的核心驱动程序包版本安装包感知驱动程序。 若要指定最低版本，请使用 INF InboxVersionRequired 指令，如以下示例中所示：

```cpp
[PrinterPackageInstallation.x86]
PackageAware=TRUE
CoreDriverDependencies={D20EA372-DD35-4950-9ED8-A6335AFE79F0}
InboxVersionRequired=<version of the updated core driver>
```

在前面的示例中，请将斜体文本替换为适当的驱动程序版本信息。

其次，使用 [**INF CopyINF 指令**](../install/inf-copyinf-directive.md) 将更新的核心驱动程序包复制到驱动程序存储区。 此指令已在 Windows Vista 中更新，以支持复制到驱动程序存储区。

完成这些步骤之后，驱动程序应准备好进行测试。 在 PnP 安装过程中，安装程序将发现新的包感知驱动程序并读取关联的 INF 文件。 CopyINF 指令将强制将更新后的核心驱动程序包加载到驱动程序存储区中，并继续执行软件包感知驱动程序安装的其余部分。

 

