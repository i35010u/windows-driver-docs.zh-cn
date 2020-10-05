---
title: 限定和分发 PSHED 插件
description: 限定和分发 PSHED 插件
ms.assetid: fe6cbb01-552f-4b24-b300-168d6311a596
keywords:
- 数字签名 WDK WHEA) ，PSHED 插件
- PSHED 插件-WHEA，资格
- PSHED 插件-WHEA，分发
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 774990a8e4a6be513601ed76a11ad16a8549148d
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732957"
---
# <a name="qualifying-and-distributing-pshed-plug-ins"></a>限定和分发 PSHED 插件


若要确保驱动程序的质量和完整性，必须对 PSHED 插件进行数字签名。 在对 PSHED 插件进行数字签名时，平台供应商必须遵循以下准则：

-   为了最大限度地缩短系统启动时间，我们建议将 [Authenticode](../install/authenticode.md) 数字签名嵌入到 PSHED 插件文件中。 有关此过程的详细信息，请参阅 [通过嵌入签名对驱动程序进行发布签名](../install/release-signing-a-driver-through-an-embedded-signature.md)。

-   在硬件平台通过服务器徽标测试过程进行额外验证之前，插件的 [驱动程序包](../install/driver-packages.md) 必须具有 Windows 硬件质量实验室 (WHQL) 数字签名。 若要获取此数字签名，必须使用 "WHQL 未分类" 测试类别来测试和提交驱动程序包。

    **注意**   无论 PSHED 插件是否是使用[Authenticode](../install/authenticode.md)数字签名嵌入的，都必须获取驱动程序包的 WHQL 数字签名。

     

有关如何对 PSHED 插件进行数字签名的详细信息，请参阅 [签署公用版驱动程序](../install/signing-drivers-for-public-release--windows-vista-and-later-.md)。

PSHED 插件获取了 WHQL 数字签名后，可以在请求系统徽标认证的任何系统中使用该插件。 有关服务器徽标认证过程的详细信息，请参阅 [Windows 徽标计划](/windows-hardware/test/hlk/)。

PSHED 插件将使用 "系列" 方法进行限定，在该方法中，可以通过一类或一系列硬件平台上的部署来限定特定 PSHED 插件。

PSHED 插件应该以类似于 BIOS 和系统固件更新分发方式的方式分配给客户。 此外，PSHED 插件应该与平台固件交互，以便可以在一系列硬件平台上部署单个 PSHED 插件。

**注意**   PSHED 插件不会通过 Windows 更新分配给客户。

 

