---
title: INF CopyINF 指令
description: CopyINF 指令会使指定的 INF 文件复制到目标系统。 Windows XP 和更高版本的 Windows 支持 CopyINF 指令。
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
ms.openlocfilehash: d8311cc88090c90c9001cd34b79e8db08ffa1e82
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733955"
---
# <a name="inf-copyinf-directive"></a>INF CopyINF 指令


**CopyINF**指令会使指定的 INF 文件复制到目标系统。 Windows XP 和更高版本的 Windows 支持 **CopyINF** 指令。

```inf
[DDInstall]
  
CopyINF=filename1.inf[,filename2.inf]...
```

<a name="remarks"></a>备注
-------

Microsoft Windows XP 和更高版本的 Windows 中提供了 **CopyINF** 指令的系统支持。

此指令通常在安装多功能设备时使用。 如果安装多功能设备需要多个 INF 文件 (对于属于多个安装程序类) 的多个函数，使用此指令可确保 Windows 在安装这些函数时将找到 INF 文件。 使用以下规则：

-   如果多功能设备提供的函数被枚举为父设备的子级 (例如 IEEE 1284.4 设备) ，则父设备的 INF 文件应具有 **CopyINF** 指令来复制设备的各个功能的 inf 文件。

-   如果多功能设备提供的所有函数 (例如 PCI 卡) 被枚举为彼此的同级，则每个函数的 INF 文件应具有一个 **CopyINF** 指令来复制所有对等函数的 inf 文件。

如果遵循这些规则，Windows 可以为每个函数安装驱动程序，而无需为每个功能提示用户提供安装磁盘。

以下几点适用于 **CopyINF** 指令：

-   在 Windows Vista 之前，Windows 会将指定的 INF 文件作为 [**DIF_INSTALLDEVICE**](./dif-installdevice.md) 的默认处理的一部分进行复制 (请参阅 [**SetupDiInstallDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiinstalldevice)) 成功安装设备后。

    Windows 将指定的 INF 文件复制到它将在设备安装过程中搜索的系统目录路径。

-   **CopyINF**指令中指定的 inf 文件必须与包含**COPYINF**指令的 inf 文件位于同一目录中。
-   你必须在多磁盘安装的每个磁盘上包含所有 INF 文件。

从 Windows Vista 开始，以下点还适用于 **CopyINF** 指令：

-   **CopyINF**指令会使指定 INF 文件引用的完整[驱动程序包](driver-packages.md)复制到[驱动程序存储区](driver-store.md)中。 这是为了支持多功能驱动程序包的部署所必需的，因为在实际安装设备时原始源媒体可能不可用。 如果指定 INF 文件引用的驱动程序包已存在于驱动程序存储区中，则将忽略在 **CopyINF** 指令中指定的 inf 文件。

-   在驱动程序存储区导入过程中（而不是在设备安装期间）处理 **CopyINF** 指令。 这意味着，在 Windows Vista 和更高版本的 Windows 上调用 [SetupCopyOEMInf](/windows/win32/api/setupapi/nf-setupapi-setupcopyoeminfa) 会导致在该时间处理指定 INF 文件中的所有 **CopyINF** 指令。 对于包含在指定 INF 文件中的每个 **CopyINF** 指令，将以递归方式发生，直到所有引用的驱动程序包都复制到驱动程序存储区中。

从 Windows 10 版本1511开始，在某些情况下 (例如，运行 Windows 更新或一些对 [**DiInstallDevice**](/windows/win32/api/newdev/nf-newdev-diinstalldevice)) 的调用），也会在适用的设备上安装 inf （通过 **CopyINF** 复制）。

有关如何复制 INF 文件的详细信息，请参阅 [复制 inf](copying-inf-files.md)。

<a name="examples"></a>示例
--------

```inf
[MyMfDevice.NTx86]
CopyINF = Sound.INF
```

