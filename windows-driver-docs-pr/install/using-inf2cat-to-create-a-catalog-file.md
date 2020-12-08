---
title: 使用 Inf2Cat 创建目录文件
description: 使用 Inf2Cat 创建目录文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c765a8545b76a9574a2cf747835b5b8f8fcc4508
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824057"
---
# <a name="using-inf2cat-to-create-a-catalog-file"></a>使用 Inf2Cat 创建目录文件


Inf2Cat 工具可用于为具有 INF 文件的任何 [驱动程序包](driver-packages.md) 创建编录文件。 有关 Inf2Cat 及其命令行参数的详细信息，请参阅 [**Inf2Cat**](../devtest/inf2cat.md)。

本主题讨论如何从驱动程序包的 INF 文件创建 [编录文件](catalog-files.md) 。 在此示例中，使用了 *toastpkg.inf* 示例驱动程序包的 INF 文件。 在 WDK 安装目录中，此 INF 文件被命名为 *toastpkg.inf* ，位于 *src \\ general \\ toaster \\ toastpkg.inf \\ INF* 目录中。

[**Inf2Cat**](../devtest/inf2cat.md)生成的目录文件的名称是通过 CatalogFile 指令指定的。 此类指令中的一个或多个在 INF 文件的 [**Inf 版本部分**](inf-version-section.md) 中声明。 *Toastpkg.inf* 文件的 "INF **版本**" 部分如下所示：

```cpp
[Version]
Signature="$WINDOWS NT$"
Class=TOASTER
ClassGuid={B85B7C50-6A01-11d2-B841-00C04FAD5171}
Provider=%ToastRUs%
DriverVer=09/21/2006,6.0.5736.1
CatalogFile.NTx86  = tostx86.cat
CatalogFile.NTIA64 = tostia64.cat
CatalogFile.NTAMD64 = tstamd64.cat
```

本 [**INF 版本部分**](inf-version-section.md)应注明两个问题：

1. [**INF 版本部分**](inf-version-section.md)声明三个不同的目录文件，每个目录文件对应驱动程序包支持的每个 Windows 版本。 执行 [**Inf2Cat**](../devtest/inf2cat.md) 时，它将为通过 **/os** 选项指定的每个 Windows 版本创建一个目录文件。

   例如，如果使用命令行参数/os： Vista_X64，则 Inf2Cat 将创建目录文件 *toastamd64.cat* 。 同样，如果使用 **/os：**<em>Vista_X86</em>选项，该工具将创建目录文件 *toastx86.cat* 。

2. INF 版本部分的 [**DriverVer 指令**](inf-driverver-directive.md) 声明旧的时间戳和版本。

   使用 [**Inf2Cat**](../devtest/inf2cat.md)之前，必须确保 INF 文件的 **DriverVer** 指令具有当前时间戳和版本值。 在测试计算机上安装和替换先前安装的包版本时， [驱动程序包](driver-packages.md) 需要此文件。

   你可以使用 [Stampinf](../devtest/stampinf.md) 工具来更新 **DriverVer** 指令中的时间戳和版本值。 例如，若要在 *toastpkg.inf* 中更新 **DriverVer** 指令，请运行以下命令 <em>：</em>

   ```cpp
   stampinf -f toastpkg.inf -d 09/01/2008 -v 9.0.9999.0
   ```

以下命令行说明了如何通过 Inf2Cat 工具使用 *toastpkg.inf* 文件创建目录文件：

```cpp
Inf2cat.exe /driver:src\general\toaster\toastpkg\toastcd\ /os:Vista_x64
```

其中：

- **/Driver** 选项指定包含一个或多个 INF 文件的目录。 在此目录中，将为包含一个或多个 CatalogFile 指令的 INF 文件创建目录文件。 有关 CatalogFile 指令的详细信息，请参阅 [**INF 版本部分**](inf-version-section.md)。

  在此示例中，只有 *TOASTPKG.INF* inf 文件位于指定的 *src \\ general \\ toaster \\ toastpkg.inf \\ toastcd* 目录中。

- **/Os：**<em>Vista_x64</em>选项指定目录文件适用于64位版本的 Windows Vista。 Inf2Cat 工具将目录文件的名称与请求的 Windows 版本相匹配。 由于 *TOASTPKG.INF* inf 文件包含具有 NTAMD64 平台扩展的 CatalogFile 指令，Inf2Cat 将创建一个名为 tstamd64.cat 的目录文件 *。*

  可以在 **/os：** 选项中指定一个或多个 Windows 版本。 例如，如果指定了 **/os：**<em>Vista_x64，Vistax32</em> ，Inf2Cat 将创建 *tstamd64.cat* 和 *tstx86.cat* 文件，因为 *CatalogFile* inf 文件中有 INF toastpkg.inf 指令。

有关该工具的命令行参数的详细信息，请参阅 [**Inf2Cat**](../devtest/inf2cat.md)。

 

