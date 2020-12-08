---
title: 验证已进行测试签名的目录文件的签名
description: 验证已进行测试签名的目录文件的签名
keywords:
- 验证测试签名
- 检查测试签名
- 目录文件 WDK 驱动程序签名，验证签名
- 测试签名目录文件 WDK
- 验证测试证书 WDK
- 测试签名驱动程序包 WDK，编录文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 569f5a6244d29496620e61e29a9f2a969d65a11c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840943"
---
# <a name="verifying-the-signature-of-a-test-signed-catalog-file"></a>验证已进行测试签名的目录文件的签名


若要验证 [驱动程序包的](driver-packages.md)[目录文件](catalog-files.md)是否已由有效的 [测试证书](./makecert-test-certificate.md)签名，请使用以下 [**SignTool**](../devtest/signtool.md)命令：

```cpp
SignTool verify /v /pa CatalogFileName.cat
```

若要验证 [驱动程序包的](driver-packages.md) 目录文件中列出的某个文件是否已由测试证书签名，请使用以下 [**SignTool**](../devtest/signtool.md) 命令：

```cpp
SignTool verify /v /pa /c CatalogFileName.cat DriverFileName
```

其中：

-   **Verify** 命令将 SignTool 配置为验证驱动程序包的目录文件的签名 *CatalogFileName.cat* 或驱动程序文件 *DriverFileName*。

-   **/V** 选项将 SignTool 配置为打印执行和警告消息。

-   **/Pa** 选项可将 SignTool 配置为验证目录文件或驱动程序文件的签名是否符合 PnP 设备安装签名要求。

-   *CatalogFileName.cat* 是驱动程序包的编录文件的名称。

-   *此*  ***/c** _ _CatalogFileName。 cat * 选项指定目录文件，其中包含文件 *DriverFileName* 的条目。

-   *DriverFileName* 是包含目录文件 *CatalogFileName.cat* 中的条目的文件的名称。

请注意，SignTool **verify** 命令不会显式指定用于对 [目录文件](catalog-files.md)进行签名的测试证书。 要使验证操作成功，您必须首先在本地计算机的 " [受信任的根证书颁发机构" 证书存储](trusted-root-certification-authorities-certificate-store.md) 中安装测试证书，该证书用于验证签名。 有关如何在本地计算机的 "受信任的根证书颁发机构" 证书存储中安装测试证书的详细信息，请参阅 [在测试计算机上安装测试证书](installing-a-test-certificate-on-a-test-computer.md)。 在签名计算机和测试计算机上，安装过程是相同的。

例如，以下命令验证 *Tstamd64.cat* 是否具有符合 windows Vista 和更高版本 Windows 的 PnP 设备安装签名要求的测试签名。 在此示例中， *Tstam64.cat* 位于运行命令的同一目录中。

```cpp
SignTool verify /v /pa tstamd64.cat
```

 

