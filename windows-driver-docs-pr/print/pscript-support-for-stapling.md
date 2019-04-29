---
title: Pscript 装钉支持
description: Pscript 装钉支持
ms.assetid: 75fc11e1-5cd9-4e95-b062-989fe493fdb5
keywords:
- 微型驱动程序 WDK Pscript 装订
- 装订 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69b6de9fd7c58fd6e8a94b1eea42017fc783c626
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359019"
---
# <a name="pscript-support-for-stapling"></a>Pscript 装钉支持





Microsoft Pscript 驱动程序支持以下标准中的功能装订*PPD*文件。

-   \*StapleLocation

-   \*StapleOrientation

-   \*StapleWhen

-   \*StapleX

-   \*StapleY

有关这些标准装订功能的详细信息，请参阅*PostScript 打印机说明文件格式规范*，版本 4.3，1996 年 2 月 9。 （此资源可能不会在某些语言和国家/地区中可用。）

若要确定设备是否支持装订，Pscript 驱动程序，请使用以下逻辑：

1.  如果没有任何装订功能上面列出的标准 PPD 文件中定义，则不支持然后装订。

2.  如果\*StapleOrientation PPD 文件中定义的唯一装订功能则支持装订。

3.  如果一个或多个以前列出标准装订功能 (而不\*StapleOrientation) 中 PPD 定义文件，如果已定义的任何的功能约束的当前配置的安装的功能，则装订不支持。 例如，如果 DuplexerUnit 可安装功能的 NotInstalled 选项上放置一个约束\*StapleLocation 和 DuplexerUnit 的打印机的当前配置为 NotInstalled，则不支持装订。

 

 




