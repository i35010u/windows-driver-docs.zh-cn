---
title: 对驱动程序包进行测试签名
description: 本部分介绍如何测试签名驱动程序包。
ms.assetid: 3BC92099-A464-4C62-9EB7-DD6AA0D1FB03
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9ac12f24d66237581ba90831b04a7da3237192ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328899"
---
# <a name="test-sign-a-driver-package"></a>对驱动程序包进行测试签名


本部分介绍如何测试签名驱动程序包。

## <a name="test-sign-a-driver-package"></a>对驱动程序包进行测试签名


使用以下步骤测试签名驱动程序包使用的测试证书：

1.  创建一个新的证书文件：

    ```console
    makecert -r -pe -ss TestCertStoreName -n "CN=WSD FabrikamV4 Driver Testing Cert" CertFileName.cer -sv CertFile.pvk
    ```

    系统将提示您输入密码。

2.  使用 pvk 文件创建 pfx 文件：

    ```console
    pvk2pfx.exe /pvk CertFile.pvk /spc CertFileName.cer /pfx CertPfx.pfx
    ```

    系统将提示您输入密码。

3.  将证书添加到计算机上的根和 trustedpublisher 证书存储位置，将安装该驱动程序。

    这使驱动程序通过在插安装过程的签名验证。 如果不执行此步骤，该驱动程序不会传递此检查，并且将无法自动安装打印机。

    ```console
    CertMgr /add CertFileName.cer /s /r localMachine root
    CertMgr /add CertFileName.cer /s /r localMachine trustedpublisher
    ```

4.  使用在步骤 2 中创建的 pfx 文件进行签名"FabrikamPrintDriverV4 包"。 其他项目不需要为此步骤中作为已签名的驱动程序是什么创建包。

有关详细信息，请参阅[如何测试签名驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/how-to-test-sign-a-driver-package)。


