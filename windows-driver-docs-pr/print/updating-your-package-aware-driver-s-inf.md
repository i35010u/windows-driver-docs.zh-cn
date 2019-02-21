---
title: 更新包识别驱动程序的 INF
description: 更新包识别驱动程序的 INF
ms.assetid: d0bf489d-d084-40df-b5aa-69cdf679993f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a58709ac71945097fb69619f9225d95bf72d788a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533946"
---
# <a name="updating-your-package-aware-drivers-inf"></a>更新包识别驱动程序的 INF


捆绑包识别驱动程序使用的核心驱动程序后下, 一步是更新包识别驱动程序的 INF 文件。

识别包的驱动程序的 INF 文件需要引用更新的核心驱动程序包。 若要执行此操作，确定核心驱动程序包与核心模型的 GUID，如中所述[编写核心驱动程序](writing-core-drivers.md)。 除了标识核心驱动程序包，需要对 INF 文件进行以下两项更改。

首先，指定核心驱动程序的最低可接受版本，以便将使用更新后的版本。 指定最低版本，则无使用核心驱动程序包的较早的不兼容版本安装的应用包识别驱动程序的可能性。 若要指定最低版本，请使用 INF InboxVersionRequired 指令，如下面的示例中所示：

```cpp
[PrinterPackageInstallation.x86]
PackageAware=TRUE
CoreDriverDependencies={D20EA372-DD35-4950-9ED8-A6335AFE79F0}
InboxVersionRequired=<version of the updated core driver>
```

在前面的示例中，将以斜体显示的文本替换相应的驱动程序版本信息。

第二种，使用[ **INF CopyINF 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547317)将更新的核心驱动程序包复制到驱动程序存储区。 此指令已在 Windows Vista 以支持将复制到驱动程序存储区中更新。

完成这些步骤后，应准备好进行测试驱动程序。 即插即用安装期间，安装程序将发现新的包识别驱动程序，并阅读相关联的 INF 文件。 CopyINF 指令将强制更新的核心驱动程序包加载到驱动程序存储区，并识别包的驱动程序安装的其余部分将继续进行。

 

 




