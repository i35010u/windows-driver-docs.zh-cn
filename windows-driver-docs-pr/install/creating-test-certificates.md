---
title: 创建测试证书
description: 创建测试证书
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7f59ae8f3ee3166fab00bdaa49af8072e926e2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827791"
---
# <a name="creating-test-certificates"></a>创建测试证书


测试签名需要测试证书。 生成测试证书后，可以使用它对多个驱动程序或 [驱动程序包](driver-packages.md)进行测试签名。 有关详细信息，请参阅 [测试证书](./makecert-test-certificate.md)。

本主题介绍如何使用 [**MakeCert**](../devtest/makecert.md) 工具创建测试证书。 在大多数开发环境中，通过 MakeCert 生成的测试证书应该足以测试测试签名驱动程序或驱动程序包的安装和加载。 有关此类测试证书的详细信息，请参阅 [MakeCert Test certificate](makecert-test-certificate.md)。

以下命令行示例使用 MakeCert 来完成以下任务：

-   *(测试)* 中创建名为 "Contoso.com" 的自签名测试证书。 此证书对使用者名称和证书颁发机构 (CA) 使用相同的名称。

-   将证书的副本放入名为 *ContosoTest* 的输出文件中。

-   将证书的副本放入名为 *PrivateCertStore* 的证书存储中。 如果将测试证书放在 *PrivateCertStore* 中，则会将其与系统上的其他证书隔离开来。

使用以下 MakeCert 命令创建 *Contoso.com (测试)* 证书：

```cmd
makecert -r -pe -ss PrivateCertStore -n CN=Contoso.com(Test) -eku 1.3.6.1.5.5.7.3.3 ContosoTest.cer
```

其中：

-   **-R** 选项创建一个自签名证书，该证书具有相同的颁发者和使用者名称。

-   **-Pe** 选项指定可以导出与证书关联的私钥。

-   **-Ss** 选项指定包含测试证书 (*PrivateCertStore*) 的证书存储的名称。

-   **-N CN =** option 指定证书的名称，Contoso.com (Test) 。 此名称与 [**SignTool**](../devtest/signtool.md) 工具一起用于标识证书。

-   EKU 选项将 (Oid) 的一个或多个以逗号分隔的 [*增强型密钥用法*](/windows/desktop/SecGloss/e-gly) 对象标识符的列表插入到证书中。 例如， `-eku 1.3.6.1.5.5.7.3.2` 插入客户端身份验证 OID。 有关允许的 Oid 的定义，请参阅 CryptoAPI 2.0 中的 Wincrypt.h 文件。

-   *ContosoTest* 是包含测试证书的副本的文件名，Contoso.com (测试) 。 证书文件用于将证书添加到 "受信任的根证书颁发机构" 证书存储和 "受信任的发布者" 证书存储中。

包含测试证书的证书存储区将添加到 Windows 在创建证书存储的开发计算机上为用户帐户管理的证书存储列表。

开发人员只需要创建一个 MakeCert 测试证书来对开发计算机上的所有 [驱动程序包](driver-packages.md) 进行签名。

有关 MakeCert 工具及其命令行参数的详细信息，请参阅 [**MakeCert**](../devtest/makecert.md)。

> [!NOTE]
> 创建测试证书后，使用 Certmgr.msc 工具将其添加到 "受信任的根证书颁发机构" 证书存储中。 有关详细信息，请参阅 [安装测试证书](installing-test-certificates.md)。

另请参阅 `Selfsign_readme.htm` `bin\selfsign` Windows 驱动程序工具包目录中的自述文件 (WDK) 。

 

