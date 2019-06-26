---
title: 如何使用打印机驱动程序 INF 文件中的修饰
description: 如何使用打印机驱动程序 INF 文件中的修饰
ms.assetid: 772e2797-8019-4715-870c-b7cd2b8e65f2
keywords:
- 多个处理器体系结构 WDK 打印机
- 基于 x86 的驱动程序示例 WDK 打印机
- 基于 Itanium 的驱动程序示例 WDK 打印机
- 未修饰的 INF WDK 打印机
- INF 文件 WDK 打印，修饰
- 修饰的 INF WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bc627d388c65e3e785f2b4dc7bc3a36732eed25
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378585"
---
# <a name="how-to-use-decorations-in-inf-files-for-printer-drivers"></a>如何使用打印机驱动程序 INF 文件中的修饰


打印机驱动程序运行的 Windows Server 2003 SP1 和更高版本，或在 64 位版本的 Windows XP 及更高版本，且面向 x64 体系结构必须包括修饰[ **INF 模型部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)所示在下面的示例。 但是，可能会作为版本的 Windows Server 2003 SP1 之前的 Windows 上的其他驱动程序安装该驱动程序，因为 INF 文件还必须提供未修饰的 INF 模型部分。 此外建议修饰用于安装基于 Itanium 的驱动程序。

以下示例演示如何编写可以用来安装适用于单个处理器体系结构的驱动程序的 INF 文件。

### <a name="x64-driver-sample"></a>x64 驱动程序示例

第一个示例演示如何使用未修饰的 INF 模型部分安装 x64 版本的 Windows XP 之前或在 x86 或基于 Itanium 的计算机运行 Windows XP 或 Windows Server 2003 上的 Windows 上的驱动程序。 在第二个 INF 模型部分 NTamd64 修饰导致 x64 驱动程序安装在任何运行 Windows Server 2003 SP1 或更高版本的处理器体系结构的计算机上。

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

下面的示例说明如何使用未修饰的 INF 模型部分的 Windows XP 之前的 Windows 版本上或在 x86 上安装的基于 Itanium 的驱动程序机正在运行 Windows XP 或 Windows Server 2003 SP1 之前。 在第二个 INF 模型部分 NTia64 修饰会导致可在任何运行 Windows Server 2003 SP1 或更高版本的处理器体系结构的计算机上安装的基于 Itanium 的驱动程序。

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

在下一步的示例中，INF 模型部分不需要修饰。 不需要指定的处理器体系结构，因为未修饰的部分都假定引用到 x86 驱动程序。 它是允许添加 INF 模型部分与 NTx86 修饰，但请记住，您还应包括的 Windows Server 2003 SP1 之前的 Windows 版本的未修饰的 INF 模型节。

```cpp
[MANUFACTURER]
%Acme Corp.% = Acme
...

[Acme]
"Acme LaserWhiz 100 PS" = Acme100_x86.PPD, <hardware IDs and compatible IDs for this printer>
```

### <a name="supporting-multiple-architectures-in-a-single-inf-file"></a>在单个的 INF 文件中支持多个体系结构

本部分演示如何编写可以用来安装多个处理器体系结构的打印机驱动程序的 INF 文件。

若要创建可以用来安装多个体系结构的驱动程序的 INF 文件，编写 INF 模型部分中，并请其根据需要任意多个副本，以便支持每个体系结构都有其自己 INF 模型部分。 在下面的示例所示，添加到每个生成的 INF 模型部分中，适当修饰每个处理器体系结构。

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

 

 




