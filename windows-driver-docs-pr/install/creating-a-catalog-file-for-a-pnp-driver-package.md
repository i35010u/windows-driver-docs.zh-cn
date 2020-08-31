---
title: 为 PnP 驱动程序包创建目录文件
description: 为 PnP 驱动程序包创建目录文件
ms.assetid: 2af431f1-a35d-4312-86f6-a928ef4148df
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 570521585591788f6a7215058c3a513e8b5f854b
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095161"
---
# <a name="creating-a-catalog-file-for-a-pnp-driver-package"></a>为 PnP 驱动程序包创建目录文件


若要为驱动程序包创建未签名的目录文件，请执行以下步骤：

1. 添加所需的 INF **CatalogFile** = <em>文件名</em>**。Cat**条目或 INF **CatalogFile。**<em>PlatformExtension</em> =<em>唯一-文件名</em>**。**[驱动程序包](driver-packages.md)inf 文件的 " [**INF 版本" 部分**](inf-version-section.md)中的 Cat 条目。 有关如何使用平台扩展的信息，请参阅 [跨平台 INF 文件](cross-platform-inf-files.md)。

2. 使用[**Inf2Cat**](../devtest/inf2cat.md)工具验证是否可以为目标平台对驱动程序包进行签名，并为应用于目标平台)  (*.cat*文件生成未签名的[目录文件](catalog-files.md)。

使用以下 Inf2Cat 命令创建未签名的目录文件：

```cpp
Inf2Cat /driver:DriverPath /os:WindowsVersionList
```

其中：

- **/Driver：**<em>DriverPath</em>参数提供[驱动程序包](driver-packages.md)所在目录的名称。

- **/Os：**<em>WindowsVersionList</em>参数将 Inf2Cat 配置为验证驱动程序包是否符合 windows 版本标识符列表指定的 windows 版本的签名要求。

### <a name="examples"></a>示例

以下示例适用于位于*c： \\ WindDDK \\ 5739 \\ src \\ general \\ toaster \\ toastpkg.inf \\ toastcd*中的 toaster[驱动程序包](driver-packages.md)。 Toaster 包的 INF 文件是 *toastpkg.inf* ，此 inf 文件包含以下包含平台扩展的 **CatalogFile** 指令：

```cpp
[Version]
. . .
CatalogFile.NTx86  = tostx86.cat
CatalogFile.NTIA64 = tostia64.cat
CatalogFile.NTAMD64 = tstamd64.cat
. . .
```

若要为特定 x86 版本的 Windows 生成 *Tostx86.cat* ，请在 *WindowsVersionList*中指定 windows 版本。 例如，以下 Inf2Cat 命令验证是否可以为 Windows 2000 和 x86 版本的 Windows Vista、Windows Server 2003 和 Windows XP 签署 [驱动程序包](driver-packages.md) 。

```cpp
Inf2Cat /driver:c:\WindDDK\5739\src\general\toaster\toastpkg\toastcd /os:2000,XP_X86,Server2003_X86,Vista_X86
```

若要为 x64 版本的 Windows 生成 *Tostamd64.cat* ，请在 *WindowsVersionList*中指定 windows 版本。 例如，以下 Inf2Cat 命令验证是否可以为 x64 版本的 Windows Vista、Windows Server 2003 和 Windows XP 签署驱动程序包。

```cpp
Inf2Cat /driver:c:\WindDDK\5739\src\general\toaster\toastpkg\toastcd /os:XP_X64,Server2003_X64,Vista_X64
```

若要仅为 Windows Vista x64 版本生成 *Tostamd64.cat* ，请仅在 WindowsVersionList 中指定 "Vista_X64" *。* 例如，以下 Inf2Cat 命令只验证是否可以为 Windows Vista x64 版本签署 [驱动程序包](driver-packages.md) 。

```cpp
Inf2Cat /driver:c:\WindDDK\5739\src\general\toaster\toastpkg\toastcd /os:Vista_X64
```

 

