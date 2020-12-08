---
title: 验证由商业证书签名的目录文件
description: 验证通过商业发布证书签名的目录文件的签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22ef10567226937cb51110c2cbf344149b5dd4b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840945"
---
# <a name="verifying-the-signature-of-a-catalog-file-signed-by-a-commercial-release-certificate"></a>验证通过商业发布证书签名的目录文件的签名


若要验证 [目录文件](catalog-files.md) 是否已由有效的 [商业发布证书](commercial-release-certificate.md)签名，请使用以下 [**SignTool**](../devtest/signtool.md) 命令：

```cpp
SignTool verify /v /pa CatalogFileName.cat
```

若要验证 [驱动程序包的](driver-packages.md) 目录文件中列出的文件是否已由有效的商业发布证书签名，请使用以下 SignTool 命令：

```cpp
SignTool verify /v /pa /c CatalogFileName.cat DriverFileName
```

其中：

-   **Verify** 命令将 SignTool 配置为验证驱动程序包的目录文件的签名 *CatalogFileName.cat* 或驱动程序文件 *DriverFileName*。

-   **/V** 选项将 SignTool 配置为打印执行和警告消息。

-   **/Pa** 选项可将 SignTool 配置为验证目录文件或驱动程序文件的签名是否符合 PnP 驱动程序安装要求。

-   *CatalogFileName.cat* 是驱动程序包的编录文件的名称。

-   *此*  ***/c** _ _CatalogFileName。 cat * 选项指定目录文件，其中包含文件 *DriverFileName* 的条目。

-   *DriverFileName* 指定包含目录文件 *CatalogFileName.cat* 中的条目的文件的名称。

 

