---
title: 为 WBDI 驱动程序签名
description: 为 WBDI 驱动程序签名
ms.assetid: 1BE83F60-4A04-457E-BD31-5E6F104A3505
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecb5a0fd99632d3fdd284fa3f1da9c4b584a0899
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095415"
---
# <a name="signing-wbdi-drivers"></a>为 WBDI 驱动程序签名


WBDI 驱动程序的特定代码签名要求取决于 WBDI 驱动程序是否是使用用户模式驱动程序框架（ (UMDF) 、内核模式驱动程序框架 (KMDF) 或 Windows 驱动模型 (WDM) 实现的。 除了需要签名的目录文件外，某些 dll 还需要使用特定属性进行签名。 有关详细信息，请参阅 [提交指纹驱动程序的步骤](/windows-hardware/design/device-experiences/windows-hello-driver-signing)。

所有 WBDI 驱动程序包必须通过 WHQL 门户进行签名，以确保其未被篡改。 无论驱动程序在内核模式下运行还是在用户模式下运行，都需要此类签名。 不需要对包中的每个文件进行签名。 相反，你可以创建一个包含包中每个文件的哈希值的编录文件，并对该目录文件进行签名。 INF 中的 CatalogFile 指令指示该文件的名称。 对于大多数 WBDI 驱动程序，目录文件签名是唯一需要的签名类型。

对于某些 WBDI 驱动程序，需要多个签名。 内核模式启动驱动程序是 Windows 加载程序在启动过程中加载的驱动程序，在 x86 和 x64 平台上都需要额外的嵌入签名。 因此，启动启动驱动程序通常必须通过两种方式进行签名：

-   与其他类型的驱动程序一样，使用 INF 安装的引导启动驱动程序包必须具有签名的目录文件。 目录文件用于安装期间的签名验证。
-   启动启动驱动程序的二进制文件必须使用具有相应交叉证书的 SPC 进行嵌入签名。 交叉证书由称为 "受信任的根) " 的 (CA 颁发，该证书用于对另一个 CA 的根证书的公钥进行签名，这会创建一个从受信任的根 CA 到多个其他 ca 的信任链。

你通常在创建并签署包的目录文件后对驱动程序二进制文件进行嵌入签名。

引导启动驱动程序具有以下特征：

-   驱动程序的 INF 将启动类型指定为 "Start = 0"。
-   内核服务配置为具有内核驱动程序或文件系统驱动程序的 **ServiceType** ，并将 **StartMode** 设置为 "boot"。


本主题不涉及驱动程序签名要求或过程的详细信息。 有关驱动程序的签名要求的常规信息，请参阅 [驱动程序签名](https://go.microsoft.com/fwlink/p/?linkid=201836)。

 

