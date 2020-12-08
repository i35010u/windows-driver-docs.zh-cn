---
title: 验证目录文件的 SPC 签名
description: 验证目录文件的 SPC 签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6c52e2094ffd821917ef1edfc09b278f62bee92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840043"
---
# <a name="verifying-the-spc-signature-of-a-catalog-file"></a>验证目录文件的 SPC 签名


若要验证 [目录文件](catalog-files.md) 是否已由有效的 [软件发行者证书签名 (SPC)](software-publisher-certificate.md) 和相应的交叉证书，请使用以下 [**SignTool**](../devtest/signtool.md) 命令：

```cpp
SignTool verify /v /kp CatalogFileName.cat 
```

若要验证[驱动程序包的](driver-packages.md)[目录文件](catalog-files.md)中列出的文件是否由[软件发行者证书 (SPC) ](software-publisher-certificate.md)和相应的交叉证书进行签名，请使用以下 SignTool 命令：

```cpp
SignTool verify /v /kp /c CatalogFileName.cat DriverFileName
```

其中：

-   **Verify** 命令将 SignTool 配置为验证 [驱动程序包](driver-packages.md)的目录文件的签名 *CatalogFileName.cat* 或驱动程序文件 *DriverFileName*。

-   **/V** 选项将 SignTool 配置为打印执行和警告消息。

-   **/Kp** 选项将 SignTool 配置为验证文件的签名是否符合 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)和 windows Vista 和更高版本的 windows 的 [PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。

-   *CatalogFileName.cat* 是驱动程序包的编录文件的名称。

-   *此*  ***/c** _ _CatalogFileName。 cat * 选项指定目录文件，其中包含文件 *DriverFileName* 的条目。

-   *DriverFileName* 是包含目录文件 *CatalogFileName.cat* 中的条目的文件的名称。

例如，以下命令验证 *Tstamd64.cat* 的数字签名是否符合内核模式代码签名策略和 windows Vista 和更高版本 Windows 的 PnP 设备安装签名要求。 在此示例中， *Tstam64.cat* 位于运行命令的同一目录中。

```cpp
SignTool verify /kp tstamd64.cat
```

在下一个示例中，以下命令验证 *toastpkg.inf* 在目录文件 *Tstamd64.cat* 中是否有条目，其数字签名符合内核模式代码签名策略和 windows Vista 和更高版本 windows 的 PnP 设备安装签名要求。 在此示例中， *Tstam64.cat* 和 *toastpkg.inf* 在运行该命令的同一目录中。

```cpp
SignTool verify /kp /c tstamd64.cat toastpkg.inf
```

 

