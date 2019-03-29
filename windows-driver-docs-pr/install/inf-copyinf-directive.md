---
title: INF CopyINF 指令
description: CopyINF 指令会导致指定的 INF 文件复制到目标系统。 在 Windows XP 和更高版本的 Windows 支持 CopyINF 指令。
ms.assetid: 289822a8-69c3-43a3-ab07-ee02a7473db8
keywords:
- INF CopyINF 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF CopyINF Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51a120bab01fffa6957f8a204cf206f5eb48a0a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565974"
---
# <a name="inf-copyinf-directive"></a>INF CopyINF 指令


一个**CopyINF**指令会导致指定的 INF 文件复制到目标系统。 **CopyINF**指令支持 Windows XP 和更高版本的 Windows 中。

```ini
[DDInstall]
  
CopyINF=filename1.inf[,filename2.inf]...
```

<a name="remarks"></a>备注
-------

系统支持**CopyINF**指令是在 Microsoft Windows XP 和更高版本的 Windows 中可用。

安装多功能设备时，通常使用此指令。 如果安装多功能设备需要多个 INF 文件 （对于属于多个安装程序类的多个函数），使用此指令可确保安装函数时，Windows 将查找的 INF 文件。 使用以下规则：

-   如果提供的多功能设备的函数作为子级的父设备 （如 IEEE 1284.4 设备） 的枚举，父设备 INF 文件应**CopyINF**指令复制 INF 文件设备的各个函数。

-   如果提供的多功能设备 （如 PCI 卡） 的所有函数的另一个对等方为都枚举，每个函数的 INF 文件应**CopyINF**指令复制 INF 文件的所有对等函数。

如果您遵循这些规则，Windows 可以安装驱动程序为每个函数，而不提示用户输入用于每个函数的安装磁盘。

以下几点适用于**CopyINF**指令：

-   在 Windows Vista 之前 Windows 会将指定的 INF 文件复制的默认处理的一部分[ **DIF_INSTALLDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff543692) (请参阅[ **SetupDiInstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552039)) 设备成功安装之后。

    Windows 将指定的 INF 文件复制到系统目录路径，它将搜索在设备安装过程。

-   中指定的 INF 文件**CopyINF**指令必须位于与包含的 INF 文件相同的目录**CopyINF**指令。
-   必须包括多磁盘安装每个磁盘上的所有 INF 文件。

从 Windows Vista 开始，以下几点也适用于**CopyINF**指令：

-   **CopyINF**指令会导致完整[驱动程序包](driver-packages.md)指定的 INF 文件，要复制到引用[驱动程序存储区](driver-store.md)。 这是支持的多功能驱动程序包，部署所必需的因为原始源介质设备实际安装时可能不可用。 如果已引用指定的 INF 文件的驱动程序包位于驱动程序存储区，INF 文件中指定**CopyINF**指令被忽略。

-   **CopyINF**设备安装过程而不是驱动程序存储区导入过程中处理指令。 这意味着，调用[SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=194252)在 Windows Vista 和更高版本的 Windows 上会导致所有**CopyINF**指定 INF 文件中的指令来处理在该时间。 发生这种情况以递归方式为每个**CopyINF**都包含在指定的 INF 文件中，直到所有被引用的驱动程序包复制到驱动程序存储区的指令。

从 Windows 10，版本 1511，在某些情况下开始 (例如，运行 Windows 更新或对某些调用[ **DiInstallDevice**](https://msdn.microsoft.com/library/windows/hardware/ff544710))，使用复制的 Inf **CopyINF**也将适用的设备上安装。

有关如何将 INF 文件复制的详细信息，请参阅[复制 Inf](copying-inf-files.md)。

<a name="examples"></a>示例
--------

```ini
[MyMfDevice.NTx86]
CopyINF = Sound.INF
```

 

 





