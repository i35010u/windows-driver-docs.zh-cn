---
title: 使用商业发布证书对目录文件进行签名
description: 使用商业发布证书对目录文件进行签名
ms.assetid: 362b0c79-50b9-4749-80e2-62601d76e9e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ccb98c77c8c7e29ffbab77d2c73edca33826f4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348769"
---
# <a name="signing-a-catalog-file-with-a-commercial-release-certificate"></a>使用商业发布证书对目录文件进行签名


使用以下[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)命令以登录[编录文件](catalog-files.md)的内核模式[驱动程序包](driver-packages.md)与[商业版本发布证书](commercial-release-certificate.md)。

**请注意**  为 32 位版本的 Windows Vista 和更高版本的 Windows，商业版本发布证书可以用于签署内核模式驱动程序在这些 Windows 版本上释放。

 

```cpp
SignTool sign /v /s CertificateStore /n CertificateName /t http://timestamp.verisign.com/scripts/timstamp.dll CatalogFileName.cat
```

其中：

-   **符号**命令将配置为对目录文件进行签名的 SignTool *CatalogFileName.cat*。

-   **/V**详细选项配置 SignTool 打印执行消息和警告消息。

-   **/S** *CertificateStore*选项指定包含的证书存储区的名称*CertificateName*证书。 按照有关如何将证书安装在系统证书存储中将证书颁发的证书颁发机构 (CA) 的说明。

-   **/N** *CertificateName*选项指定在证书的名称*CertificateStore*证书存储区。

-   **/T**   * http://timestamp.verisign.com/scripts/timstamp.dll *选项提供 VeriSign 提供的公开可用的时间戳服务器的 URL。

-   *CatalogFileName.cat*目录文件的名称。

 

 





