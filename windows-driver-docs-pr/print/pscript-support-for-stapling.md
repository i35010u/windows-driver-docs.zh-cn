---
title: Pscript 装钉支持
description: Pscript 装钉支持
keywords:
- 微型驱动程序 WDK Pscript，装订
- 装订 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e32c3a32b2c7b38f5673dabeb5d42f06b67f68ed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807143"
---
# <a name="pscript-support-for-stapling"></a>Pscript 装钉支持





Microsoft Pscript 驱动程序支持 *PPD* 文件中的以下标准装订功能。

-   \*StapleLocation

-   \*StapleOrientation

-   \*StapleWhen

-   \*StapleX

-   \*StapleY

有关这些标准装订功能的详细信息，请参阅 *PostScript 打印机说明文件格式规范*，版本4.3，9月9日1996。  (此资源可能在某些语言和国家/地区不可用。 ) 

为了确定设备是否支持装订，Pscript 驱动程序使用以下逻辑：

1.  如果在 PPD 文件中未定义以前列出的任何标准装订功能，则不支持装订。

2.  如果 \* StapleOrientation 是 PPD 文件中定义的唯一装订功能，则支持装订。

3.  如果在 PPD 文件中定义了一个或多个以前列出的标准装订功能 (而不是 \* StapleOrientation) ，并且任何定义的功能受可安装功能的当前配置的限制，则不支持装订。 例如，如果 DuplexerUnit 可安装功能的 NotInstalled 选项在 StapleLocation 上放置了一个约束 \* ，并且该打印机的 DuplexerUnit 的当前配置为 NotInstalled，则不支持装订。

 

 




