---
title: MakeCert 测试证书
description: MakeCert 测试证书
ms.assetid: 17f63c42-a563-4a57-a3be-ac3b2e97ee3b
keywords:
- MakeCert test 证书 WDK
- 数字证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd08d4902adcd404cab6904fb91c0bbc924b9ffd
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097393"
---
# <a name="makecert-test-certificate"></a>MakeCert 测试证书


MakeCert 测试证书是使用[**MakeCert**](../devtest/makecert.md)工具创建的[x.509 数字证书](digital-certificates.md)。 MakeCert 测试证书是一个自签名根证书，可用于对[驱动程序包的](driver-packages.md)[目录文件](catalog-files.md)进行测试签名或通过在驱动程序文件中嵌入签名来对驱动程序文件进行测试签名。

若要了解有关创建 MakeCert 测试证书的详细信息，请参阅 [**创建测试证书**](creating-test-certificates.md)。

## <a name="installing-a-makecert-test-certificate"></a>安装 MakeCert 测试证书

若要对 [目录文件](catalog-files.md) 进行测试签名或将签名嵌入驱动程序文件中，MakeCert 测试证书可以位于个人证书存储中 ( "我的" 存储) 或其他一些自定义证书存储区，用于对软件进行签名。 但是，若要验证测试签名，则必须在用于验证签名的本地计算机的 " [受信任的根证书颁发机构" 证书存储](trusted-root-certification-authorities-certificate-store.md) 中安装相应的测试证书。

使用 [**certmgr.msc**](../devtest/certmgr.md) 工具，如下所示，在用于签署驱动程序的本地计算机的 "受信任的根证书颁发机构" 证书存储中安装测试证书：

```cpp
CertMgr /add CertFileName.cer /s /r localMachine root
```

必须在受信任的根证书颁发机构证书存储和测试计算机的 "[受信任的发布者" 证书存储](trusted-publishers-certificate-store.md)中安装测试证书，然后才能安装由 MakeCert 测试证书签名的[驱动程序包](driver-packages.md)。 有关如何在测试计算机上安装 MakeCert 测试证书的信息，请参阅 [在测试计算机上安装测试证书](installing-a-test-certificate-on-a-test-computer.md)。

 

