---
title: 验证已发布签名驱动程序文件的签名
description: 验证已发布签名驱动程序文件的签名
ms.assetid: 70876389-6493-4c16-8a82-ca72fc23325c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dadda4e302a79b3fba8699a06f0c82885286b2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547459"
---
# <a name="verifying-the-signature-of-a-release-signed-driver-file"></a>验证已发布签名驱动程序文件的签名


若要验证创建的驱动程序文件中的嵌入式的签名[软件发布者证书 (SPC)](software-publisher-certificate.md)，使用以下[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)命令：

```cpp
SignTool verify /v /kp DriverFileName.sys
```

其中：

-   **验证**命令将配置 SignTool 验证签名的驱动程序文件中嵌入*DriverFileName.sys。*

-   **/V**选项配置 SignTool 打印执行消息和警告消息。

-   **/Kp**选项配置 SignTool 验证中嵌入签名*DriverFileName.sys*符合[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)和[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)适用于 Windows Vista 和更高版本的 Windows。

-   *DriverFileName.sys*是驱动程序文件的名称。

例如，以下命令验证*Toaster.sys*具有有效的嵌入的签名。 在此示例中，T*oaster.sys*处于*amd64*在其中运行命令的目录下的子目录。

```cpp
SignTool verify /kp amd64\toaster.sys
```

 

 





