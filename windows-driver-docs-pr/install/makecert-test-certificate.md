---
title: MakeCert 测试证书
description: MakeCert 测试证书
ms.assetid: 17f63c42-a563-4a57-a3be-ac3b2e97ee3b
keywords:
- MakeCert 测试证书 WDK
- 数字证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3afd2840c513ca2c904a4e03bb84c051ba442026
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377665"
---
# <a name="makecert-test-certificate"></a>MakeCert 测试证书


MakeCert 测试证书是否[X.509 数字证书](digital-certificates.md)通过使用创建[ **MakeCert** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/makecert)工具。 MakeCert 测试证书是自签名的根证书，可用于测试签名[驱动程序包](driver-packages.md)[编录文件](catalog-files.md)或测试签名的驱动程序文件中嵌入签名的驱动程序文件。

若要了解有关创建 MakeCert 测试证书的详细信息，请参阅[**创建测试证书**](creating-test-certificates.md)。

## <a name="installing-a-makecert-test-certificate"></a>安装 MakeCert 测试证书

对测试签名[编录文件](catalog-files.md)或驱动程序文件中嵌入签名，MakeCert 测试证书可以是个人证书存储区 （"my"存储中） 或其他自定义证书存储，对进行签名的本地计算机软件。 但是，若要验证的测试签名，相应的测试证书必须安装在[受信任的根证书颁发机构证书存储区](trusted-root-certification-authorities-certificate-store.md)用于验证签名的本地计算机。

使用[ **CertMgr** ](../devtest/certmgr.md)工具，如下所示，在用于签署驱动程序在本地计算机的受信任的根证书颁发机构证书存储中安装测试证书：

```cpp
CertMgr /add CertFileName.cer /s /r localMachine root
```

在安装之前[驱动程序包](driver-packages.md)MakeCert 测试证书签名，必须在受信任的根证书颁发机构证书存储区中安装测试证书和[受信任发布服务器的证书存储](trusted-publishers-certificate-store.md)的测试计算机。 有关如何在测试计算机上安装 MakeCert 测试证书的信息，请参阅[测试计算机上安装测试证书](installing-a-test-certificate-on-a-test-computer.md)。

 

 





