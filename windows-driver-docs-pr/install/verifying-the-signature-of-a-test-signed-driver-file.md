---
title: 验证已进行测试签名的驱动程序文件的签名
description: 验证已进行测试签名的驱动程序文件的签名
ms.assetid: 21f4c42c-3d6e-453c-acff-f4b8acc3e20b
keywords:
- 测试签名驱动程序文件 WDK
- 验证测试签名
- 检查测试签名
- 测试签名 WDK
- 验证测试证书 WDK
- 驱动程序文件的测试签名 WDK
- 测试签名驱动程序包 WDK，驱动程序文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e923126bbf0a19944589be54d8bd86af3e44728
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339296"
---
# <a name="verifying-the-signature-of-a-test-signed-driver-file"></a>验证已进行测试签名的驱动程序文件的签名


若要验证的测试签名的驱动程序文件中嵌入，请使用以下[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)命令：

```cpp
SignTool verify /v /pa DriverFileName.sys
```

其中：

-   **验证**命令将配置 SignTool 验证签名的驱动程序文件中嵌入*DriverFileName.sys。*

-   **/V**选项配置 SignTool 要打印的执行和警告消息。

-   **/Pa**选项配置 SignTool 验证中嵌入签名*DriverFileName.sys*符合即插即用设备安装签名要求。

-   *DriverFileName.sys*是驱动程序文件的名称。

请注意，SignTool**验证**命令未显式指定用于签名的驱动程序文件的测试证书。 若要成功验证操作，您必须首先安装中的测试证书[受信任的根证书颁发机构证书存储区](trusted-root-certification-authorities-certificate-store.md)用于验证签名的本地计算机。 有关如何在本地计算机的受信任的根证书颁发机构证书存储中安装测试证书的详细信息，请参阅[测试计算机上安装测试证书](installing-a-test-certificate-on-a-test-computer.md)。 安装过程是签名的计算机和一台测试计算机上相同。

例如，以下命令验证中的嵌入的签名*Toaster.sys*，后者位于*amd64*在其中运行命令的目录下的子目录。

```cpp
SignTool verify /v /pa amd64\toaster.sys
```

 

 





