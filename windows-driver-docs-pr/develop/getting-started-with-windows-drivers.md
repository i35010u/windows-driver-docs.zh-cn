---
ms.assetid: E109BD80-F9CB-4F1F-A6FD-1142E27EC6AD
title: Windows 驱动程序入门
description: 使用 Windows 驱动程序，可以创建一个同时在 Windows 10X 和 Windows 桌面版中运行的驱动程序。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: b2039ae8d30b9de3f55aa8e52f80441ba6e1c854
ms.sourcegitcommit: 9fe9c8309690fd8fe7af50865d3ac216887ab922
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85071689"
---
# <a name="getting-started-with-windows-drivers"></a>Windows 驱动程序入门

自 Windows 10 版本 2004 发布后的某个时间点起，在 Windows 中运行的驱动程序被归类为 Windows 驱动程序或 Windows 桌面驱动程序。 

Windows 驱动程序在所有 Window 10 变体中运行，其中包括 Windows 10X 和 Windows 10 桌面版。  Windows 桌面驱动程序只在 Windows 10 桌面版中运行。  

“Windows 驱动程序”分类将扩展并取代当前的“通用驱动程序”分类。 

此页面提供了即将发布的 Windows 驱动程序要求的预览。  

> [!NOTE]
> Windows 驱动程序和 Windows 桌面驱动程序之间的区别并不影响任何要为 Windows 10 版本 2004 提交和认证的驱动程序。  认证和提交方面的变更将在以后进行。


## <a name="windows-drivers-requirements"></a>Windows 驱动程序要求

当 Windows 驱动程序成为认证选项时，需要遵守以下要求：

- 符合 [DCH 设计原则](dch-principles-best-practices.md)。
- 遵循[驱动程序包隔离](driver-isolation.md)原则。
- 遵循 [API 分层要求](api-layering.md)。
- 使用 [Hardware Lab Kit](https://docs.microsoft.com/windows-hardware/test/hlk/) 获得 [Windows 硬件兼容性计划认证流程](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-certification-process)认证。 请注意，Windows 硬件兼容性计划认证流程要求适用于 KMDF 和 UMDF 驱动程序。

## <a name="windows-drivers-vs-windows-desktop-drivers"></a>Windows 驱动程序与Windows 桌面驱动程序

下表总结了上述区别：

|                                                                     |Windows 驱动程序|Windows 桌面驱动程序 |
| --------------------------------------------------------------------|:-------------:|:----------------------:|
| 在 Windows 10 桌面版中运行                                           | 是           | 是                    |
| 在 Windows 10X 中运行                                                  | 是           | 否                     |
| 必须获得 WHCP 认证                                         | 是           | 否                     |
| WDK 和 HLK 是开发和认证驱动程序的主要工具| 是           | 是                    |
| 遵循更严格的可靠性和可维护性要求（如驱动程序包隔离）     | 是           | 否                     |


尽管只在 Windows 10 桌面版中运行的驱动程序不需要符合针对 Windows 驱动程序的附加要求，但这样做将增强驱动程序的可维护性和可靠性，并为将来可能在 Windows 10X 上获得认证做好准备。
