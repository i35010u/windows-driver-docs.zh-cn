---
title: 在 Windows 更新上为生物识别驱动程序排名
description: 在 Windows 更新上为生物识别驱动程序排名
ms.assetid: fc8634ab-0ecd-4390-9834-825f60fe68ce
keywords:
- 生物识别驱动程序 WDK，Windows Update 上排名
- 排名生物识别驱动程序 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76f287e954c65e1d1205b0db3a80ed425816a64c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566556"
---
# <a name="ranking-a-biometric-driver-on-windows-update"></a>在 Windows 更新上为生物识别驱动程序排名


提供这两个生物识别的旧的供应商和 WBDI 驱动程序可以使用驱动程序功能分数来控制从 Windows 更新安装的驱动程序。

供应商都选择编写单个驱动程序支持旧版查询语言和 WBDI 应注意，若要正确使用 Windows 生物识别框架，该驱动程序必须支持独占访问权限。 当禁用独占访问权限时，该驱动程序充当旧驱动程序。 若要查看如何在注册表中设置独占值，请参阅[安装生物识别驱动程序](installing-a-biometric-driver.md)。

此外，在旧模式下运行的生物识别驱动程序不应分配 GUID\_DEVINTERFACE\_生物识别\_读取器设备接口。 分配此设备接口会导致 Windows 生物识别服务识别驱动程序。

如果正确设置了特征评分，将仅在不具有生物识别驱动程序已在位置的系统上安装 WBDI 驱动程序。

如果客户决定选择使用旧堆栈，客户可以通过 WBDI 驱动程序安装排名更高版本的旧驱动程序。

### <a name="span-idhowfeaturescoreworksspanspan-idhowfeaturescoreworksspanhow-feature-score-works"></a><span id="how_feature_score_works"></span><span id="HOW_FEATURE_SCORE_WORKS"></span>功能分数的工作原理是如何

功能分数都表示总体的驱动程序级别的第三个和第四个数字中。 例如， *GG*是从以下驱动程序级别的功能得分：

```cpp
0x00GG0000 
```

较低的功能数字指示更好的匹配项。 默认功能得分是 0xff 内，指示没有首选项基于驱动程序的功能。

Microsoft 建议 0xa0 旧生物识别驱动程序的特征评分。 功能分数应永远不会设置为 0x00，，以防出现需要更高版本重写它。

由一个 INF FeatureScore 指令中设置驱动程序的功能得分[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)设备。

例如，下面的代码设置为 0x20 驱动程序的功能得分：

```cpp
[DDInstallSectionName]
. . .
FeatureScore=x20
```

有关如何在驱动程序上设置特征评分的详细信息，请参阅[特征评分 (Windows Vista)](https://go.microsoft.com/fwlink/p/?linkid=132806)。

 

 





