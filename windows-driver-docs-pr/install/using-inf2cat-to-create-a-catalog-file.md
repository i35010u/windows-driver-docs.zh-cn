---
title: 使用 Inf2Cat 创建目录文件
description: 使用 Inf2Cat 创建目录文件
ms.assetid: 93dea980-eb66-40f0-ac6b-0adaf8376154
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea029f19a656ba32313198b889eba0d1b3c7f03d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522653"
---
# <a name="using-inf2cat-to-create-a-catalog-file"></a>使用 Inf2Cat 创建目录文件


Inf2Cat 工具可用于创建目录文件的任何[驱动程序包](driver-packages.md)具有 INF 文件。 有关 Inf2Cat 和其命令行自变量的详细信息，请参阅[ **Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089)。

**请注意**  之前 Windows Server 2008 Windows Driver Kit (WDK)，Inf2Cat 工具不是 WDK 工具的一部分。 但是，该工具随 Winqual 提交工具。 若要下载的 Winqual 提交工具，请转到 Microsoft [Inf2Cat 常见问题解答](https://go.microsoft.com/fwlink/p/?linkid=79443)网站。 安装 Winqual 提交工具包时， [ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)放在 Program Files (x86)\\系统驱动器上的 Microsoft Winqual Submission Tool 文件夹。

 

本主题介绍了如何创建[编录文件](catalog-files.md)从驱动程序包的 INF 文件。 在此示例中的 INF 文件*ToastPkg*使用示例驱动程序包。 在 WDK 安装目录中，此 INF 文件被命名为*toastpkg.inf* ，它位于*src\\常规\\toaster\\toastpkg\\inf*目录。

文件的目录名称的[ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)通过 CatalogFile 指令指定生成。 中声明一个或多个这些指令[ **INF 版本部分**](inf-version-section.md)的 INF 文件。 INF**版本**一部分*toastpkg.inf*文件如下所示：

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

有关此应注意两件事情[ **INF 版本部分**](inf-version-section.md):

1. [ **INF 版本部分**](inf-version-section.md)声明三个不同的目录文件，分别对应于每个驱动程序包支持的 Windows 版本。 当[ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)是执行，会创建一个目录文件为每个 Windows 版本，通过指定 **/os**选项。

   例如，Inf2Cat 创建编录文件*toastamd64.cat*如果使用命令行参数 /os:Vista_X64。 同样，该工具将创建目录文件*toastx86.cat*如果 **/os:**<em>Vista_X86</em>使用选项。

2. [ **DriverVer 指令**](inf-driverver-directive.md) INF 版本的部分用于声明应用旧时间戳和版本。

   在使用之前[ **Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089)，必须确保 INF 文件**DriverVer**指令具有当前的时间戳和版本值。 这必需[驱动程序包](driver-packages.md)安装并替换以前安装的测试计算机上的包版本。

   可以使用[Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)工具来更新的时间戳和版本值以**DriverVer**指令。 例如，若要更新**DriverVer**指令*toastpkg.inf*，运行以下命令<em>:</em>

   ```cpp
   stampinf -f toastpkg.inf -d 09/01/2008 -v 9.0.9999.0
   ```

下面的命令行演示如何通过使用创建编录文件的 Inf2Cat 工具通过*Toastpkg.inf*文件：

```cpp
Inf2cat.exe /driver:src\general\toaster\toastpkg\toastcd\ /os:Vista_x64
```

其中：

- **/Driver**选项指定的目录，其中包含一个或多个 INF 文件。 在此目录中，为那些包含一个或多个 CatalogFile 指令的 INF 文件创建目录文件。 有关 CatalogFile 指令的详细信息，请参阅[ **INF 版本部分**](inf-version-section.md)。

  在此示例中，仅*toastpkg*.inf INF 文件是否位于指定*src\\常规\\toaster\\toastpkg\\toastcd*目录。

- **/Os:**<em>Vista_x64</em>选项指定为 64 位版本的 Windows Vista 是目录文件。 Inf2Cat 工具将匹配到请求的 Windows 版本的编录文件的名称。 由于*toastpkg*.inf INF 文件包含带有 NTAMD64 平台扩展名的 CatalogFile 指令，Inf2Cat 将创建名为一个目录文件*tstamd64.cat。*

  可以在中指定一个或多个 Windows 版本 **/os:** 选项。 例如，如果 **/os:**<em>Vista_x64、 Vistax32</em>指定，则将创建 Inf2Cat *tstamd64.cat*并*tstx86.cat*文件，因为中的 INF CatalogFile 指令*toastpkg*.inf INF 文件。

有关该工具的命令行参数的详细信息，请参阅[ **Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089)。

 

 





