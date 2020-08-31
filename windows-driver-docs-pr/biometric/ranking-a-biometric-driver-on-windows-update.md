---
title: 在 Windows 更新上为生物识别驱动程序排名
description: 在 Windows 更新上为生物识别驱动程序排名
ms.assetid: fc8634ab-0ecd-4390-9834-825f60fe68ce
keywords:
- 生物识别驱动程序 WDK，Windows 更新排名
- 排名生物识别驱动程序 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37df547662f378510284310f8b61f6979e6459e7
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095417"
---
# <a name="ranking-a-biometric-driver-on-windows-update"></a>在 Windows 更新上为生物识别驱动程序排名

提供旧版生物识别和 WBDI 驱动程序的供应商可以使用驱动程序功能评分来控制从 Windows 更新安装的驱动程序。

选择写入支持旧版本和 WBDI 的单个驱动程序的供应商应该知道，若要在 Windows Biometric Framework 上正常工作，驱动程序必须支持独占访问。 禁用独占访问时，驱动程序将作为旧驱动程序运行。 若要查看如何在注册表中设置独占值，请参阅 [安装生物识别驱动程序](installing-a-biometric-driver.md)。

此外，在传统模式下操作的生物识别驱动程序不应分配 GUID \_ DEVINTERFACE \_ 生物识别 \_ 读卡器设备接口。 分配此设备接口会导致 Windows 生物识别服务识别该驱动程序。

如果已正确设置功能分数，则 WBDI 驱动程序将仅安装在未安装有生物识别驱动程序的系统上。

如果客户决定选择加入旧堆栈，则客户可以通过 WBDI 驱动程序安装更高级别的旧驱动程序。

## <a name="how-feature-score-works"></a>功能分数的工作原理

功能分数以整体驱动程序排名的第三位和第四位数表示。 例如， *GG* 是来自以下驱动程序级别的功能分数：

```cpp
0x00GG0000
```

较小的特征号表示更匹配。 默认功能分数为0xFF，这表示没有基于驱动程序功能的首选项。

对于传统生物识别驱动程序，Microsoft 建议使用0xa0 的功能分数。 如果需要在以后重写功能评分，则绝不应将其设置为0x00。

驱动程序的功能分数由设备的 [**Inf DDInstall 部分**](../install/inf-ddinstall-section.md) 中的 inf FeatureScore 指令设置。

例如，以下代码将驱动程序的功能分数设置为0x20：

```cpp
[DDInstallSectionName]
. . .
FeatureScore=x20
```

有关如何在驱动程序上设置功能分数的详细信息，请参阅 [功能分数](../install/feature-score--windows-vista-and-later-.md)。