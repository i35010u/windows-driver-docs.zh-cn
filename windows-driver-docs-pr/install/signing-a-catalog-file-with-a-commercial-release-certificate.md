---
title: 使用商业发布证书对目录文件进行签名
description: 使用商业发布证书对目录文件进行签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e035aba02862a079eb9699ae9b0781b398e6621
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793587"
---
# <a name="signing-a-catalog-file-with-a-commercial-release-certificate"></a>使用商业发布证书对目录文件进行签名

使用以下 [**SignTool**](../devtest/signtool.md)命令通过 [商业版本证书](commercial-release-certificate.md)对内核模式 [驱动程序包](driver-packages.md)的 [目录文件](catalog-files.md)进行签名。

>[!NOTE]
>对于32位版本的 Windows Vista 和更高版本的 Windows，只能使用商业版本证书对要在这些 Windows 版本上发布的内核模式驱动程序进行签名。

```cpp
SignTool sign /v /s CertificateStore /n CertificateName /t http://timestamp.digicert.com CatalogFileName.cat
```

其中：

- **Sign** 命令将 SignTool 配置为对编录文件 *CatalogFileName.cat* 进行签名。

- **/V** verbose 选项将 SignTool 配置为打印执行和警告消息。

- **/S** *CertificateStore* 选项指定包含 *CertificateName* 证书的证书存储区的名称。 按照颁发证书的证书颁发机构 (CA) 的说明，了解如何在系统证书存储中安装证书。

- **/N** *CertificateName* 选项指定 *CertificateStore* 证书存储区中的证书名称。

- **/T** `http://timestamp.digicert.com` 选项提供 DigiCert 提供的公开可用的时间戳服务器的 URL。  

- *CatalogFileName.cat* 是目录文件的名称。
