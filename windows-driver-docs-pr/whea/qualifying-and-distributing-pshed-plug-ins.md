---
title: 限定和分发 PSHED 插件
description: 限定和分发 PSHED 插件
ms.assetid: fe6cbb01-552f-4b24-b300-168d6311a596
keywords:
- 数字签名 WDK WHEA），PSHED 插件
- PSHED 插件 WDK WHEA，符合条件的
- PSHED 插件 WDK WHEA，分发
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f409665dc7d3f3890032e1bc2fee31f16671a189
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387153"
---
# <a name="qualifying-and-distributing-pshed-plug-ins"></a>限定和分发 PSHED 插件


若要确保质量和驱动程序的完整性，PSHED 插件必须进行数字签名。 进行数字签名 PSHED 插件时，平台供应商必须遵循以下准则：

-   若要最大程度减少系统启动时，我们建议嵌入[Authenticode](https://docs.microsoft.com/windows-hardware/drivers/install/authenticode)到 PSHED 插件文件的数字签名。 有关此过程的详细信息，请参阅[版本签名的驱动程序通过嵌入式签名](https://docs.microsoft.com/windows-hardware/drivers/install/release-signing-a-driver-through-an-embedded-signature)。

-   硬件平台可以进行其他验证通过 server 徽标测试之前进行处理，即插即用接[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)必须具有 Windows 硬件质量实验室 (WHQL) 数字签名。 若要获取此数字签名，必须测试和使用 WHQL 未分类的测试类别提交的驱动程序包。

    **请注意**  必须获取 WHQL 数字签名的驱动程序包，而不考虑是否使用嵌入插件 PSHED [Authenticode](https://docs.microsoft.com/windows-hardware/drivers/install/authenticode)数字签名。

     

有关如何进行数字签名 PSHED 插件的详细信息，请参阅[公开发布的版本的签名驱动程序](https://docs.microsoft.com/windows-hardware/drivers/install/signing-drivers-for-public-release--windows-vista-and-later-)。

PSHED 插件获取 WHQL 数字签名后，该插件可在为其请求系统徽标认证的任何系统。 有关 server 徽标认证过程的详细信息，请参阅[Windows 徽标计划](https://go.microsoft.com/fwlink/p/?linkid=26144)。

将使用"系列"的方法，其中特定 PSHED 插件可以限定为部署在类或系列的硬件平台之间限定 PSHED 插件。

PSHED 插件应由硬件供应商以类似于 BIOS 和系统固件更新如何分布的方式分发给客户。 此外，应使用单个 PSHED 插件，可以部署在系列的硬件平台的方式在平台固件接口 PSHED 插件。

**请注意**  PSHED 插件未被分发到客户通过 Windows 更新。

 

 

 




