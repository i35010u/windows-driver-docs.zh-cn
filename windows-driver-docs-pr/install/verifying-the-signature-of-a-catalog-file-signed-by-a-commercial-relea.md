---
title: 验证由商业证书签名的编录文件
description: 验证签名的商业版本发布证书签名的编录文件
ms.assetid: 153bb1e7-009d-4ef8-b5d7-a9e6eecf65bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1780998634cbbe23211e080ef8c6012fdd1512b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554601"
---
# <a name="verifying-the-signature-of-a-catalog-file-signed-by-a-commercial-release-certificate"></a>验证签名的商业版本发布证书签名的编录文件


若要确认[编录文件](catalog-files.md)由有效签名[商业版本发布证书](commercial-release-certificate.md)，使用以下[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)命令：

```cpp
SignTool verify /v /pa CatalogFileName.cat
```

若要验证的文件中列出[驱动程序包的](driver-packages.md)由有效的商业版本发布证书签名的编录文件，请使用以下 SignTool 命令：

```cpp
SignTool verify /v /pa /c CatalogFileName.cat DriverFileName
```

其中：

-   **验证**命令将配置 SignTool 验证驱动程序包的目录文件的签名*CatalogFileName.cat*或驱动程序文件*DriverFileName*。

-   **/V**选项配置 SignTool 打印执行消息和警告消息。

-   **/Pa**选项配置 SignTool 验证编录文件或驱动程序文件的签名符合即插即用驱动程序安装要求。

-   *CatalogFileName.cat*是驱动程序包的编录文件的名称。

-    ***/C*** *CatalogFileName.cat*选项指定包含该文件的条目的目录文件*DriverFileName*。

-   *DriverFileName*指定的文件的目录文件中有条目的名称*CatalogFileName.cat*。

 

 





