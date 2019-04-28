---
title: 验证目录文件的 SPC 签名
description: 验证目录文件的 SPC 签名
ms.assetid: 57bc65fe-1c31-4ebb-a1bc-e1fe275f8d10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45ae9e413b8d0e42ed7040684606c2792470d1be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339299"
---
# <a name="verifying-the-spc-signature-of-a-catalog-file"></a>验证目录文件的 SPC 签名


若要确认[编录文件](catalog-files.md)由有效签名[软件发行者证书 (SPC)](software-publisher-certificate.md)和相应交叉证书，使用以下[ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)命令：

```cpp
SignTool verify /v /kp CatalogFileName.cat 
```

若要验证的中列出的文件[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)由签名[软件发行者证书 (SPC)](software-publisher-certificate.md)和相应交叉证书使用以下 SignTool 命令：

```cpp
SignTool verify /v /kp /c CatalogFileName.cat DriverFileName
```

其中：

-   **验证**命令将配置 SignTool 验证的签名[驱动程序包](driver-packages.md)编录文件*CatalogFileName.cat*或驱动程序文件*DriverFileName*。

-   **/V**选项配置 SignTool 打印执行消息和警告消息。

-   **/Kp**选项配置 SignTool 验证文件签名符合[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)和[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)的 Windows Vista 和更高版本的 Windows。

-   *CatalogFileName.cat*是驱动程序包的编录文件的名称。

-    ***/C*** *CatalogFileName.cat*选项指定包含该文件的条目的目录文件*DriverFileName*。

-   *DriverFileName*编录文件中有条目的文件的名称*CatalogFileName.cat*。

例如，以下命令验证*Tstamd64.cat*具有符合内核模式代码签名策略和即插即用设备安装签名要求适用于 Windows Vista 及更高版本的数字签名Windows 的版本。 在此示例中， *Tstam64.cat*是在其中运行该命令的相同目录中。

```cpp
SignTool verify /kp tstamd64.cat
```

在下一步的示例中，以下命令验证*Toastpkg.inf*，这在编录文件中没有条目*Tstamd64.cat*，具有符合内核模式代码签名的数字签名策略和签名要求的 Windows Vista 和更高版本的 Windows 即插即用设备安装。 在此示例中， *Tstam64.cat*并*Toastpkg.inf*是在其中运行该命令的相同目录中。

```cpp
SignTool verify /kp /c tstamd64.cat toastpkg.inf
```

 

 





