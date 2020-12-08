---
title: 如何使用打印机驱动程序 INF 文件中的修饰
description: 如何使用打印机驱动程序 INF 文件中的修饰
keywords:
- 多处理器体系结构 WDK 打印机
- 基于 x86 的驱动程序示例 WDK 打印机
- 基于 Itanium 的驱动程序示例 WDK 打印机
- 未修饰的 INF WDK 打印机
- INF 文件 WDK 打印，装饰品
- 修饰 INF WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31e5b2ee0c74acc02247ade6f8dfe944c14c29c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835827"
---
# <a name="how-to-use-decorations-in-inf-files-for-printer-drivers"></a>如何使用打印机驱动程序 INF 文件中的修饰


在 Windows Server 2003 上运行的使用 SP1 和更高版本的打印机驱动程序，或在 Windows XP 和更高版本的64位版本上运行的打印机驱动程序，并且目标 x64 体系结构必须包括修饰的 [**INF 模型部分**](../install/inf-models-section.md) ，如以下示例中所示。 但是，因为在 Windows Server 2003 SP1 之前，驱动程序可能作为附加驱动程序安装在 Windows 版本上，因此 INF 文件还必须提供未修饰的 INF 模型部分。 还建议使用装饰来安装基于 Itanium 的驱动程序。

下面的示例演示如何编写可用于为单处理器体系结构安装驱动程序的 INF 文件。

### <a name="x64-driver-sample"></a>x64 驱动程序示例

第一个示例演示如何使用未修饰的 INF 模型部分在 Windows XP 之前的 Windows 版本上或在运行 Windows XP 或 Windows Server 2003 的基于 x86 或基于 Itanium 的计算机上安装 x64 驱动程序。 "第二个 INF 模型" 部分中的 NTamd64 修饰会导致在运行带有 SP1 或更高版本的 Windows Server 2003 的任何处理器体系结构的计算机上安装 x64 驱动程序。

```cpp
[MANUFACTURER]
%Acme Corp.% = Acme, NTamd64
...

[Acme]
"Acme LaserWhiz 100 PS" = Acme100_x64.PPD, <hardware IDs and compatible IDs for this printer>

[Acme.NTamd64]
"Acme LaserWhiz 100 PS" = Acme100_x64.PPD, <hardware IDs and compatible IDs for this printer>
```

### <a name="itanium-based-driver-sample"></a>基于 Itanium 的驱动程序示例

下一个示例演示如何使用未修饰的 INF 模型部分在 Windows XP 之前的 Windows 版本上或在 SP1 之前运行 Windows XP 或 Windows Server 2003 的 x86 计算机上安装基于 Itanium 的驱动程序。 "第二个 INF 模型" 部分中的 NTia64 修饰会使基于 Itanium 的驱动程序安装在运行 Windows Server 2003 SP1 或更高版本的任何处理器体系结构的计算机上。

```cpp
[MANUFACTURER]
%Acme Corp.% = Acme, NTia64
...

[Acme]
"Acme LaserWhiz 100 PS" = Acme100_ia64.PPD, <hardware IDs and compatible IDs for this printer>

[Acme.NTia64]
"Acme LaserWhiz 100 PS" = Acme100_ia64.PPD, <hardware IDs and compatible IDs for this printer>
```

### <a name="x86-driver-sample"></a>x86 驱动程序示例

在下一个示例中，"INF 模型" 部分不需要修饰。 不需要指定处理器体系结构，因为假定未修饰的部分引用 x86 驱动程序。 允许使用 NTx86 修饰添加 INF 模型部分，但请记住，在 Windows Server 2003 SP1 之前，还应包含 Windows 版本的未修饰 INF 模型部分。

```cpp
[MANUFACTURER]
%Acme Corp.% = Acme
...

[Acme]
"Acme LaserWhiz 100 PS" = Acme100_x86.PPD, <hardware IDs and compatible IDs for this printer>
```

### <a name="supporting-multiple-architectures-in-a-single-inf-file"></a>在一个 INF 文件中支持多个体系结构

本部分介绍如何编写可用于为多处理器体系结构安装打印机驱动程序的 INF 文件。

若要创建可用于为多个体系结构安装驱动程序的 INF 文件，请编写一个 INF 模型部分，并根据需要创建它的任意数量的副本，以便每个受支持的体系结构都具有自己的 INF 模型部分。 将每个处理器体系结构的相应修饰添加到每个生成的 INF 模型部分，如下面的示例所示。

```cpp
[MANUFACTURER]
%Acme Corp% = Acme, NTamd64, NTia64
...

;; Used to install
;;    - a driver of any architecture type, on a machine running Windows 2000
;;    - a driver of any architecture type, on an x86 machine running Windows XP or Windows Server 2003
;;    - an x86 driver on a machine of any architecture type, running Windows Server 2003 with SP1
[Acme]
%Acme Model 1% = Acme100PS, <hardware IDs and compatible IDs for this printer>

;; Used to install
;;    - an x64 driver on a machine of any architecture type, running Windows Server 2003 with SP1
[Acme.NTamd64]
%Acme Model 1% = Acme100PS, <hardware IDs and compatible IDs for this printer>

;; Used to install
;;    - a driver of any architecture type, on an Itanium-based machine running Windows XP or Windows Server 2003
;;    - an Itanium-based driver on a machine of any architecture type, running Windows Server 2003 with SP1
[Acme.NTia64]
%Acme Model 1% = Acme100PS, <hardware IDs and compatible IDs for this printer>

;; DDInstall Section. 
;; This sample assumes that all three versions of the driver 
;; use the same DDInstall section.
[Acme100PS]
CopyFiles = MyDriverFile.dll, ...

[DestinationDirs]
DefaultDestDir=66000

[SourceDisksNames.x86]
1= %Location%,,,

[SourceDisksFiles.x86]
MyDriverFile.dll = 1,\i386
...

[SourceDisksNames.amd64]
1= %Location%,,,

[SourceDisksFiles.amd64]
MyDriverFile.dll = 1,\amd64
...

[SourceDisksNames.ia64]
1= %Location%,,,

[SourceDisksFiles.ia64]
MyDriverFile.dll = 1,\ia64
...

[Strings]
Acme Corp = "Acme Corporation"
Acme Model 1 = "Acme LaserWhiz 100 PS"
Location = "Acme CD ROM"
```

 

