---
title: Windows 如何对驱动程序分级
description: Windows 如何对驱动程序分级
ms.assetid: 54b6f40a-e5f6-41dd-8876-c9f0fb36ee00
keywords:
- 排名 WDK 设备安装的驱动程序
- 排名 WDK 设备安装的驱动程序
- 驱动程序选择 WDK 设备安装，排名驱动程序
- 查找设备安装 WDK 设备安装，排名驱动程序的驱动程序
- 搜索在设备安装 WDK 设备驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3486ed018fcf84947682336fc87274459ce55b51
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386283"
---
# <a name="how-windows-ranks-drivers"></a>Windows 如何对驱动程序分级


Windows 将分配给设备相匹配的驱动程序的排名。 等级表示驱动程序与设备匹配的程度。 驱动程序级别等于或大于零的整数表示。 越低排名，更好的匹配驱动程序是用于设备。

驱动程序的排名是复合值的依赖于驱动程序的签名、 支持的驱动程序和之间的匹配项的类型的功能[设备标识字符串](device-identification-strings.md)的报告的设备和设备中的条目指定的标识字符串[ **INF 模型部分**](inf-models-section.md)的驱动程序 INF 文件。

由类型为 DWORD 的值表示排名。 排名是签名分数、 功能得分和标识符得分的总和。 排名格式化为 0x*SSGGTHHH*，其中*S*， *G*， *T*，并*H*是四位域和*SS*， *GG*，并*THHH*字段表示三个排名分数，按如下所示：

-   [签名分数](signature-score--windows-vista-and-later-.md)排名基于它的签名是否受信任的驱动程序。 签名分数仅取决于的值*SS*字段。 未指定的签名分数表示为 0x*SS*0000000。

    有关如何 Windows Vista 和更高版本的 Windows 使用的驱动程序签名来确定如何安装该驱动程序的概述，请参阅[签名类别和驱动程序安装](signature-categories-and-driver-installation.md)。

-   [功能分数](feature-score--windows-vista-and-later-.md)排名基于该驱动程序支持的功能的驱动程序。 仅上的值取决于特征评分*GG*字段。 未指定的功能分数表示为 0x00*GG*0000。

-   [标识符分数](identifier-score--windows-vista-and-later-.md)排名之间的匹配项的类型的驱动程序[设备标识字符串](device-identification-strings.md)的报告的设备和 INF 的条目中列出的设备标识字符串*模型*驱动程序 INF 文件部分。 标识符分数仅取决于的值*THHH*字段。 未指定的标识符分数表示为 0x0000*THHH*。

指示一个驱动程序和驱动程序签名的类型的秩 SetupAPI 日志中的项的信息，请参阅[SetupAPI 日志中的驱动程序级别信息](driver-rank-information-in-the-setupapi-log.md)。

 

 





