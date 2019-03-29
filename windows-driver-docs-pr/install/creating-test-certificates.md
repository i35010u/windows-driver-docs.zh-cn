---
title: 创建测试证书
description: 创建测试证书
ms.assetid: 4e6daa96-029c-4e1c-b483-b900cb836858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb5da0a1585b825404a27ffe197fc08867b197ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575802"
---
# <a name="creating-test-certificates"></a>创建测试证书


测试签名需要测试证书。 生成测试证书后，它可以是用于测试登录多个驱动程序或[驱动程序包](driver-packages.md)。 有关详细信息，请参阅[测试证书](test-certificates.md)。

本主题介绍如何使用[ **MakeCert** ](https://msdn.microsoft.com/library/windows/hardware/ff548309)工具来创建测试证书。 在大多数开发环境中，通过 MakeCert 生成的测试证书应足以测试的安装和加载测试签名的驱动程序或驱动程序包。 有关此类型的测试证书的详细信息，请参阅[MakeCert 的测试证书](makecert-test-certificate.md)。

下面的命令行示例使用 MakeCert 来完成以下任务：

-   创建一个名为的自签名的测试证书*Contoso.com(Test)*。 此证书使用相同的名称的使用者名称和证书颁发机构 (CA)。

-   将证书的副本放在名为输出文件*ContosoTest.cer*。

-   将证书的副本放在名为的证书存储中*PrivateCertStore*。 将测试证书放入*PrivateCertStore*保持独立于其他可能会在系统的证书。

使用以下 MakeCert 命令来创建*Contoso.com(Test)* 证书：

```cpp
makecert -r -pe -ss PrivateCertStore -n CN=Contoso.com(Test) -eku 1.3.6.1.5.5.7.3.3 ContosoTest.cer
```

其中：

-   **-R**选项具有相同的颁发者和使用者名称创建一个自签名的证书。

-   **-Pe**选项指定与证书相关联的私钥可导出。

-   **-Ss**选项指定包含测试证书的证书存储区的名称 (*PrivateCertStore*)。

-   **-N CN =** 选项指定的证书，Contoso.com(Test) 的名称。 此名称用于[ **SignTool** ](../devtest/signtool.md)工具找到的证书。

-   EKU 选项限制到代码签名的最终证书的使用情况。

-   *ContosoTest.cer*是包含测试证书，Contoso.com(Test) 的副本的文件名。 证书文件用于将证书添加到受信任的根证书颁发机构证书存储和受信任的发行者证书存储区。

包含测试证书的证书存储区添加到其创建的证书存储在开发计算机上的用户帐户的 Windows 管理的证书存储的列表。

开发人员必须创建只有一个 MakeCert 测试证书来签署所有[驱动程序包](driver-packages.md)开发计算机上。

有关 MakeCert 工具和其命令行自变量的详细信息，请参阅[ **MakeCert**](https://msdn.microsoft.com/library/windows/hardware/ff548309)。

此外请参阅自述文件*Selfsign_readme.htm*中*bin\\selfsign* Windows 驱动程序工具包 (WDK) 的目录。

 

 





