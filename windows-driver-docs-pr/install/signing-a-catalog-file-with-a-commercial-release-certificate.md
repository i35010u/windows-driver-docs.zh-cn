---
title: 使用商业发布证书对目录文件进行签名
description: 使用商业发布证书对目录文件进行签名
ms.assetid: 362b0c79-50b9-4749-80e2-62601d76e9e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f42fea9e76753988760af4e1de1e390b3e5aa555
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025303"
---
# <a name="signing-a-catalog-file-with-a-commercial-release-certificate"></a>使用商业发布证书对目录文件进行签名


使用以下[**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)命令通过[商业版本证书](commercial-release-certificate.md)对内核模式[驱动程序包](driver-packages.md)的[目录文件](catalog-files.md)进行签名。

**注意对于 32**位版本的 windows Vista 和更高版本的 windows, 只有商用版本证书可用于对要在这些 Windows 版本上发布的内核模式驱动程序进行签名。  

 

```cpp
SignTool sign /v /s CertificateStore /n CertificateName /t http://timestamp.digicert.com CatalogFileName.cat
```

其中：

-   **Sign**命令将 SignTool 配置为对编录文件*CatalogFileName.cat*进行签名。

-   **/V** verbose 选项将 SignTool 配置为打印执行和警告消息。

-   **/S** *CertificateStore*选项指定包含*CertificateName*证书的证书存储区的名称。 按照颁发证书的证书颁发机构 (CA) 的说明, 了解如何在系统证书存储中安装证书。

-   **/N** *CertificateName*选项指定*CertificateStore*证书存储区中的证书名称。

-   **/T**   *http://timestamp.digicert.com* 选项提供 VeriSign 提供的公开可用的时间戳服务器的 URL。

-   *CatalogFileName.cat*是目录文件的名称。

 

 





