---
title: Windows 如何对驱动程序分级
description: Windows 如何对驱动程序分级
ms.assetid: 54b6f40a-e5f6-41dd-8876-c9f0fb36ee00
keywords:
- 排名驱动程序 WDK 设备安装
- 驱动程序排名 WDK 设备安装
- 驱动程序选择 WDK 设备安装，排名驱动程序
- 查找设备安装 WDK 设备安装的驱动程序，排名驱动程序
- 在设备安装期间搜索驱动程序 WDK 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a568bac6c4e0f5f56302190e8a552cb730079445
ms.sourcegitcommit: 70830486331e3ca0f550e5ddf8c42ad7ac782841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91813711"
---
# <a name="how-windows-ranks-drivers"></a>Windows 如何对驱动程序分级

> [!NOTE]
> 此页介绍 Windows 如何确定与设备匹配的给定驱动程序的驱动程序排名值。  若要了解驱动程序的排名和其他因素 (包括 INF 日期、驱动程序版本 ) 等），请参阅 windows [如何选择驱动](./overview-of-the-driver-selection-process.md#-how-windows-selects-drivers)程序。

Windows 为与设备匹配的驱动程序分配一个级别。 排名指示驱动程序与设备的匹配程度。 驱动程序排名由大于或等于零的整数表示。 排名越低，设备的驱动程序匹配就越好。

驱动程序的排名是一个组合值，它取决于驱动程序的签名、驱动程序支持的功能，以及设备报告的设备 [标识字符串](device-identification-strings.md) 与驱动程序 inf 文件的 " [**INF 模型" 部分**](inf-models-section.md) 中指定的设备标识字符串之间的匹配类型。

秩由 DWORD 类型的值表示。 排名是签名分数、特征分数和标识符分数的总和。 Rank 的格式为 0x*SSGGTHHH*，其中 *S*、 *G*、 *T*和 *H* 为四位域， *SS*、 *GG*和 *THHH* 字段表示三个排名分数，如下所示：

-   [签名分数](signature-score--windows-vista-and-later-.md)根据其签名是否可信来对驱动程序进行排名。 签名分数仅依赖于 *SS* 字段的值。 未指定的签名分数表示为 0x*SS*0000000。

    有关 Windows Vista 和更高版本的 Windows 如何使用驱动程序的签名来确定驱动程序的安装方式的概述，请参阅 [签名类别和驱动程序安装](signature-categories-and-driver-installation.md)。

-   [功能分数](feature-score--windows-vista-and-later-.md)基于驱动程序支持的功能对驱动程序进行排名。 功能分数仅依赖于 " *GG* " 字段的值。 未指定的特征分数表示为 0x00*GG*0000。

-   [标识符分数](identifier-score--windows-vista-and-later-.md)根据设备报告的[设备标识字符串](device-identification-strings.md)与驱动程序 INF 文件的 "INF*模型*" 部分中列出的设备标识字符串之间的匹配类型对驱动程序进行排名。 标识符分数仅依赖于 *THHH* 字段的值。 未指定的标识符分数表示为 0x0000*THHH*。

有关 Setupapi.log 日志中指示驱动程序的排名和驱动程序签名类型的项的信息，请参阅 [Setupapi.log 日志中的驱动程序排名信息](driver-rank-information-in-the-setupapi-log.md)。

 

 





