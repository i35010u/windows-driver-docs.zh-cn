---
title: 安装测试证书
description: 安装测试证书
ms.assetid: 4c306390-32cc-4c7a-9f61-48e8af385a6d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbd67a9ce610e2b3167791182dae5d20ce09d613
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544008"
---
# <a name="installing-test-certificates"></a>安装测试证书


若要成功安装测试签名[驱动程序包](driver-packages.md)的测试计算机上，计算机必须能够验证签名。 为此，请测试计算机必须具有证书颁发机构 (CA) 颁发计算机的受信任的根证书颁发机构证书存储中安装的包的测试证书的证书

CA 证书必须一次只能添加到受信任的根证书颁发机构证书存储。 添加后，它可验证所有驱动程序或驱动程序包已进行数字签名证书后之前在计算机上安装驱动程序包, 的签名。

若要将测试证书添加到受信任的根证书颁发机构证书存储的最简单方法是通过[ **CertMgr** ](https://msdn.microsoft.com/library/windows/hardware/ff543411)工具。 本主题将介绍安装测试证书，Contoso.com(test) 的过程。 此证书存储中*ContosoTest.cer*文件。 有关如何创建此证书的详细信息，请参阅[创建测试证书](creating-test-certificates.md)。

以下命令行使用 Certmgr.exe 安装或，Contoso.com(test) 将证书添加到测试计算机的受信任的根证书颁发机构证书存储：

```cpp
certmgr.exe /add ContosoTest.cer /s /r localMachine root
```

其中：

-   / 添加选项指定的证书*ContosoTest.cer*文件是要添加到指定的证书存储区。

-   **/S**选项指定的证书，则将添加到系统存储。

-   /R 选项指定的系统存储位置，为*currentUser*或*localMachine*。

-   *根*指定为本地计算机的目标存储区名称***根***来指定受信任的根证书颁发机构证书存储或***trustedpublisher***来指定受信任的发行者证书存储。

证书复制到受信任的根证书颁发机构证书存储区后，你可以查看通过 Microsoft 管理控制台 (MMC) 证书管理单元中，如中所述[查看测试证书](viewing-test-certificates.md)。

下面的屏幕截图显示 Contoso.com(Test) 证书的受信任的根证书颁发机构证书存储中。

![受信任的根证书颁发机构证书的屏幕截图将存储在证书 mmc 管理单元](images/certstore2.png)

有关 CertMgr 和其命令行自变量的详细信息，请参阅[ **CertMgr**](https://msdn.microsoft.com/library/windows/hardware/ff543411)。

有关如何安装测试证书的详细信息，请参阅[测试计算机上安装测试证书](installing-a-test-certificate-on-a-test-computer.md)。

 

 





