---
title: 安装测试证书
description: 安装测试证书
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 629a0a691b215a1d33c90f773f7ef864f2973ac2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839517"
---
# <a name="installing-test-certificates"></a>安装测试证书


若要成功在测试计算机上安装测试签名的 [驱动程序包](driver-packages.md) ，计算机必须能够验证该签名。 为此，测试计算机必须具有证书颁发机构的证书 (CA) 在计算机的受信任根证书颁发机构证书存储中安装了包的测试证书

必须将 CA 证书添加到 "受信任的根证书颁发机构" 证书存储中。 添加后，可以在计算机上安装驱动程序包之前，使用它来验证所有驱动程序或驱动程序包的签名（使用证书进行数字签名）。

将测试证书添加到 "受信任的根证书颁发机构" 证书存储的最简单方法是使用 [**certmgr.msc**](../devtest/certmgr.md) 工具。 本主题将介绍安装测试证书、Contoso.com (测试) 的过程。 此证书存储在 *ContosoTest* 文件中。 有关如何创建此证书的详细信息，请参阅 [创建测试证书](creating-test-certificates.md)。

以下命令行使用 Certmgr.exe 来安装或添加 Contoso.com (测试) 证书添加到测试计算机的 "受信任的根证书颁发机构" 证书存储：

```cpp
certmgr /add ContosoTest.cer /s /r localMachine root
```

其中：

-   /Add 选项指定 *ContosoTest* 文件中的证书将添加到指定的证书存储中。

-   **/S** 选项指定将证书添加到系统存储中。

-   /R 选项指定系统存储位置，该位置为 *currentUser* 或 *localMachine*。

-   *Root* 指定本地计算机的目标存储的名称，该名称可以是 ***Root** _ 来指定受信任的根证书颁发机构证书存储，也可以指定 _*_trustedpublisher_*_ 来指定受信任的发布者证书存储。

成功的运行将生成以下输出：

```cmd
certmgr /add ContosoTest.cer /s /r localMachine root
CertMgr Succeeded
```

将证书复制到本地计算机的根存储 ("受信任的根证书颁发机构" 证书存储区后) _not，可以通过 Microsoft 管理控制台 (MMC) 证书 "管理单元查看该证书，如 [查看测试证书](viewing-test-certificates.md)中所述。

以下屏幕截图显示了 "受信任的根证书颁发机构" 证书存储中的 Contoso.com (测试) 证书。

![mmc "证书" 管理单元中 "受信任的根证书颁发机构" 证书存储的屏幕截图](images/certstore2.png)

你还可以在命令提示符处查看该证书：

```cmd
certutil -store root | findstr Contoso
certutil -store root <SHA-1 id of certificate>
```

或者，从 PowerShell：

```cmd
Get-ChildItem -path cert: \LocalMachine\My | findstr Contoso
```

Certmgr.exe 工具是 Windows SDK 的一部分，通常安装到 `C:\Program Files (x86)\Windows Kits\10\bin\<build>\x86\certmgr.exe` 。

有关 Certmgr.msc 及其命令行参数的详细信息，请参阅 [**certmgr.msc**](../devtest/certmgr.md)。

有关如何安装测试证书的详细信息，请参阅 [在测试计算机上安装测试证书](installing-a-test-certificate-on-a-test-computer.md)。

 

