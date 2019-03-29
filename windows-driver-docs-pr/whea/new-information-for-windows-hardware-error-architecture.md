---
title: Windows 硬件错误体系结构的新信息
description: Windows 硬件错误体系结构的新信息
ms.assetid: 258dca19-3988-4fab-bc9f-a93035cbbd0e
keywords:
- Windows 硬件错误体系结构 WDK，新的信息
- WHEA WDK，新的信息
- 硬件错误 WDK WHEA，新的信息
- 错误 WDK WHEA，WHEA 有关的新信息
- 源信息 WDK WHEA 新
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c4aa9a92bdf0eb746b84916d5f5e9d4861ac6e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575994"
---
# <a name="new-information-for-windows-hardware-error-architecture"></a>Windows 硬件错误体系结构的新信息


本部分总结了主要新增功能和修订版本为 Windows 硬件错误体系结构 (WHEA)。 在本部分中的每个主题介绍对于每个 Windows 操作系统版本到 WHEA 中做的更改。

本部分包括以下主题：

[WHEA 更改适用于 Windows Server 2008 和 Windows Vista SP1](whea-changes-for-windows-server-2008-and-windows-vista-sp1.md)

[Windows 7 的 WHEA 更改](whea-changes-for-windows-7.md)

## <a name="new-whea-changes-for-windows8"></a>(*新*) 适用于 Windows 8 的 WHEA 更改


从 Windows 8 开始，以下进行了更改到 Windows 硬件错误体系结构 (WHEA)

-   新的 WMI 提供程序类[ **WHEAPolicyManagementMethods**](https://msdn.microsoft.com/library/windows/hardware/hh451252)。
-   WHEA 策略可以是托管类型但[ **WHEAPolicyManagementMethods** ](https://msdn.microsoft.com/library/windows/hardware/hh451252)或通过 WHEA Powershell 模块。 如果通过任一这些模式进行了更新策略，策略值将立即生效。
-   WHEA WMI 方法[ **WHEAErrorSourceMethods::SetErrorSourceInfoRtn** ](https://msdn.microsoft.com/library/windows/hardware/ff559531)已弃用。

 

 




