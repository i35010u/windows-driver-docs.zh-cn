---
title: 为 PnP 驱动程序包创建目录文件
description: 为 PnP 驱动程序包创建目录文件
ms.assetid: 2af431f1-a35d-4312-86f6-a928ef4148df
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa946915d6035f4f3384909b956008c812c36654
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365480"
---
# <a name="creating-a-catalog-file-for-a-pnp-driver-package"></a>为 PnP 驱动程序包创建目录文件


若要创建驱动程序包的未签名的编录文件，请执行以下步骤：

1. 添加所需的 INF **CatalogFile**=<em>FileName</em> **。Cat**条目或 INF **CatalogFile。** <em>PlatformExtension</em>=<em>唯一文件名</em> **。Cat**条目[ **INF 版本部分**](inf-version-section.md)的[驱动程序包的](driver-packages.md)INF 文件。 有关如何使用平台扩展的信息，请参阅[跨平台 INF 文件](cross-platform-inf-files.md)。

2. 使用[ **Inf2Cat** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat)工具来验证是否可以为目标平台签名的驱动程序包并生成无符号[编录文件](catalog-files.md)( *.cat*文件)，适用于目标平台。

使用以下的 Inf2Cat 命令，以创建未签名的编录文件：

```cpp
Inf2Cat /driver:DriverPath /os:WindowsVersionList
```

其中：

- **/Driver:** <em>DriverPath</em>参数提供的目录的名称，[驱动程序包](driver-packages.md)所在。

- **/Os:** <em>WindowsVersionList</em>参数配置 Inf2Cat 以验证驱动程序包是否符合指定的 Windows 系列的 Windows 版本的签名要求版本标识符。

### <a name="examples"></a>示例

下面的示例适用于 toaster[驱动程序包](driver-packages.md)位于*c:\\WindDDK\\5739\\src\\常规\\toaster\\toastpkg\\toastcd*。 Toaster 程序包的 INF 文件是*Toastpkg.inf* ，且此 INF 文件包含以下**CatalogFile**指令与平台扩展：

```cpp
[Version]
. . .
CatalogFile.NTx86  = tostx86.cat
CatalogFile.NTIA64 = tostia64.cat
CatalogFile.NTAMD64 = tstamd64.cat
. . .
```

若要生成*Tostx86.cat*为特定的 x86 版本的 Windows，指定中的 Windows 版本*WindowsVersionList*。 例如，以下 Inf2Cat 命令确认[驱动程序包](driver-packages.md)进行签名的 Windows 2000 和 x86 版本的 Windows Vista、 Windows Server 2003 和 Windows XP。

```cpp
Inf2Cat /driver:c:\WindDDK\5739\src\general\toaster\toastpkg\toastcd /os:2000,XP_X86,Server2003_X86,Vista_X86
```

若要生成*Tostamd64.cat*针对 x64 版本的 Windows，指定中的 Windows 版本*WindowsVersionList*。 例如，以下 Inf2Cat 命令验证是否可以进行驱动程序包签名针对 x64 版本的 Windows Vista、 Windows Server 2003 和 Windows XP。

```cpp
Inf2Cat /driver:c:\WindDDK\5739\src\general\toaster\toastpkg\toastcd /os:XP_X64,Server2003_X64,Vista_X64
```

若要生成*Tostamd64.cat*仅对于 Windows Vista x64 Edition，仅"Vista_X64"指定*WindowsVersionList。* 例如，以下 Inf2Cat 命令只验证[驱动程序包](driver-packages.md)进行签名的 Windows Vista x64 Edition。

```cpp
Inf2Cat /driver:c:\WindDDK\5739\src\general\toaster\toastpkg\toastcd /os:Vista_X64
```

 

 





