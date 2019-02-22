---
title: 验证测试签名的目录文件的签名
description: 验证测试签名的目录文件的签名
ms.assetid: fa627f5b-977e-49ca-b099-358ed686eef7
keywords:
- 验证测试签名
- 检查测试签名
- 目录文件 WDK 驱动程序签名，验证签名
- 测试签名目录文件 WDK
- 验证测试证书 WDK
- 测试签名驱动程序包 WDK，目录文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71e7622aa7d62cb9292ab0bd316a4b9c2e4d58cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547102"
---
# <a name="verifying-the-signature-of-a-test-signed-catalog-file"></a>验证测试签名的目录文件的签名


若要确认[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)由有效签名[测试证书](test-certificates.md)，使用以下[ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)命令：

```cpp
SignTool verify /v /pa CatalogFileName.cat
```

若要验证文件中列出[驱动程序包](driver-packages.md)目录文件，是由测试证书签名，使用以下[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)命令：

```cpp
SignTool verify /v /pa /c CatalogFileName.cat DriverFileName
```

其中：

-   **验证**命令将配置 SignTool 验证驱动程序包的目录文件的签名*CatalogFileName.cat*或驱动程序文件*DriverFileName*。

-   **/V**选项配置 SignTool 打印执行消息和警告消息。

-   **/Pa**选项配置 SignTool 验证编录文件或驱动程序文件的签名符合即插即用设备安装签名要求。

-   *CatalogFileName.cat*是驱动程序包的编录文件的名称。

-    ***/C*** *CatalogFileName.cat*选项指定包含该文件的条目的目录文件*DriverFileName*。

-   *DriverFileName*编录文件中有条目的文件的名称*CatalogFileName.cat*。

请注意，SignTool**验证**命令未显式指定用于签名的测试证书[编录文件](catalog-files.md)。 若要成功验证操作，您必须首先安装中的测试证书[受信任的根证书颁发机构证书存储区](trusted-root-certification-authorities-certificate-store.md)用于验证签名的本地计算机。 有关如何在本地计算机的受信任的根证书颁发机构证书存储中安装测试证书的详细信息，请参阅[测试计算机上安装测试证书](installing-a-test-certificate-on-a-test-computer.md)。 安装过程是签名的计算机和一台测试计算机上相同。

例如，以下命令验证*Tstamd64.cat*符合签名要求的 Windows Vista 和更高版本的 Windows 即插即用设备安装的测试签名。 在此示例中， *Tstam64.cat*是在其中运行该命令的相同目录中。

```cpp
SignTool verify /v /pa tstamd64.cat
```

 

 





