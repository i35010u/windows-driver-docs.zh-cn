---
title: INF InboxVersionRequired 指令
description: INF InboxVersionRequired 指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5665b222eb8bb0148122d2b939e42d1f8104d36e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835693"
---
# <a name="inf-inboxversionrequired-directive"></a>INF InboxVersionRequired 指令


对于可识别程序包的驱动程序，可以使用 **InboxVersionRequired** inf 指令为 INF 所引用的所有核心驱动程序指定可接受的最低版本。 可以使用 **UseDriverVer** 关键字指定最低版本。 此最低版本适用于 INF 中引用的所有核心驱动程序。

以下示例包感知驱动程序部分显示了如何插入 **InboxVersionRequired** INF 指令：

```cpp
[PrinterPackageInstallation.amd64]
PackageAware=TRUE
CoreDriverDependencies={D20EA372-DD35-4950-9ED8-A6335AFE79F0},{D20EA372-DD35-4950-9ED8-A6335AFE79F3}
InboxVersionRequired=UseDriverVer
```

如果使用 **UseDriverVer** 关键字作为 **InboxVersionRequired** 的值，则 **UseDriverVer** 将通知类安装程序使用 INF 中的 **DriverVer** 指令版本字符串，该版本被分析为任何核心驱动程序的最低可接受版本。 使用 **UseDriverVer** 关键字的驱动程序时，必须谨慎。 INF 引用的所有核心驱动程序必须是相同或更高的版本，安装才能成功。

你还可以将特定版本字符串指定为 **InboxVersionRequired** 的值。 这些版本字符串与 [**INF 版本部分**](../install/inf-version-section.md)中指定的 **DriverVer** 字符串遵循相同的格式。 有关 **DriverVer** 字符串格式的详细信息，请参阅 [**INF DriverVer 指令**](../install/inf-driverver-directive.md)。

下面的示例演示如何将 **InboxVersionRequired** 设置为特定版本字符串：

```cpp
InboxVersionRequired=09/28/1999,5.00.2136.1
```

 

