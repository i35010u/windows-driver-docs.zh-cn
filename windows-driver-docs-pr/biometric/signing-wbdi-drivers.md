---
title: 为 WBDI 驱动程序签名
description: 为 WBDI 驱动程序签名
ms.assetid: 1BE83F60-4A04-457E-BD31-5E6F104A3505
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfd484b2aac839ec3227de9f0fde097b245cf6c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328365"
---
# <a name="signing-wbdi-drivers"></a>为 WBDI 驱动程序签名


WBDI 驱动程序的特定代码签名要求取决于是否使用用户模式驱动程序框架 (UMDF)、 内核模式驱动程序框架 (KMDF) 或 Windows 驱动程序模型 (WDM) 实现 WBDI 驱动程序。 除了需要进行签名的编录文件，某些 dll 需要使用特定的属性进行签名。 有关详细信息，请参阅[提交指纹驱动程序的步骤](https://docs.microsoft.com/windows-hardware/design/device-experiences/windows-hello-driver-signing)。

必须通过 WHQL 门户中，签名 WBDI 的所有驱动程序包，以确保它已不被篡改。 这种签名是必需的驱动程序运行在内核模式下或在用户模式下。 不需要在包中的每个单个文件进行签名。 相反，创建包含在包中，每个文件的哈希值的目录文件和目录文件进行签名。 INF 在 CatalogFile 指令指示该文件的名称。 对于大多数 WBDI 驱动程序，目录文件签名是签名的唯一所需的类型。

对于某些 WBDI 驱动程序，需要使用多个签名。 内核模式引导启动驱动程序，它是 Windows 加载程序在启动过程中加载的驱动程序，需要在 x86 和 x64 平台上的其他嵌入式的签名。 因此，通常必须通过两种方式签名的引导启动驱动程序：

-   使用 INF 安装的引导启动驱动程序包必须具有签名的编录文件，就像其他类型的驱动程序。 编录文件用于在安装过程中的签名验证。
-   引导启动驱动程序的二进制文件必须是通过一个 SPC 使用相应的交叉证书中嵌入签名。 交叉证书是由另一个 CA，为多个其他 Ca 从单一的受信任的根 CA 创建的信任链的根证书的公钥进行签名的 CA （称为受信任的根） 颁发的。

您通常嵌入签名的驱动程序二进制文件后创建和包的目录文件进行签名。

引导启动驱动程序具有以下特征：

-   驱动程序的 INF 中指定的启动类型为"启动 = 0"。
-   内核服务配置了**ServiceType**内核驱动程序或文件系统驱动程序的和已**StartMode**设置为"启动"。


本主题不涉及驱动程序签名要求或过程的详细信息。 有关驱动程序签名要求的常规信息，请参阅[驱动程序签名](https://go.microsoft.com/fwlink/p/?linkid=201836)。

 

 





