---
title: 验证已进行测试签名的驱动程序文件的签名
description: 验证已进行测试签名的驱动程序文件的签名
keywords:
- 测试签名驱动程序文件 WDK
- 验证测试签名
- 检查测试签名
- 测试签名 WDK
- 验证测试证书 WDK
- 驱动程序文件测试签名 WDK
- 测试签名驱动程序包 WDK，驱动程序文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77ac543b69de015ce01d9d517e7f3b122fa9a3ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840941"
---
# <a name="verifying-the-signature-of-a-test-signed-driver-file"></a>验证已进行测试签名的驱动程序文件的签名


若要验证嵌入驱动程序文件的测试签名，请使用以下 [**SignTool**](../devtest/signtool.md) 命令：

```cpp
SignTool verify /v /pa DriverFileName.sys
```

其中：

-   **Verify** 命令将 SignTool 配置为验证嵌入驱动程序文件DriverFileName.sys 中的签名 *。*

-   **/V** 选项将 SignTool 配置为打印执行和警告消息。

-   **/Pa** 选项可将 SignTool 配置为验证 *DriverFileName.sys* 中嵌入的签名是否符合 PnP 设备安装签名要求。

-   *DriverFileName.sys* 是驱动程序文件的名称。

请注意，SignTool **verify** 命令不会显式指定用于对驱动程序文件进行签名的测试证书。 要使验证操作成功，您必须首先在本地计算机的 " [受信任的根证书颁发机构" 证书存储](trusted-root-certification-authorities-certificate-store.md) 中安装测试证书，该证书用于验证签名。 有关如何在本地计算机的 "受信任的根证书颁发机构" 证书存储中安装测试证书的详细信息，请参阅 [在测试计算机上安装测试证书](installing-a-test-certificate-on-a-test-computer.md)。 在签名计算机和测试计算机上，安装过程是相同的。

例如，下面的命令验证 *Toaster.sys* 中嵌入的签名，该签名位于运行命令的目录下的 *amd64* 子目录中。

```cpp
SignTool verify /v /pa amd64\toaster.sys
```

 

