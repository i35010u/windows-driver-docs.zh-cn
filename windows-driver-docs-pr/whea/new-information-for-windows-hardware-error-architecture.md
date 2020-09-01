---
title: Windows 硬件错误体系结构的新信息
description: Windows 硬件错误体系结构的新信息
ms.assetid: 258dca19-3988-4fab-bc9f-a93035cbbd0e
keywords:
- Windows 硬件错误体系结构 WDK，新信息
- WHEA WDK，新信息
- 硬件错误 WDK WHEA，新信息
- 错误 WDK WHEA，有关 WHEA 的新信息
- 源信息 WDK WHEA，新
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fb16a0d0c3cece6ae4a29944b04eebf1065d26d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216312"
---
# <a name="new-information-for-windows-hardware-error-architecture"></a>Windows 硬件错误体系结构的新信息


本部分概述了 Windows 硬件错误体系结构的主要新增内容和修订 (WHEA) 。 本部分中的每个主题描述对每个 Windows 操作系统版本的 WHEA 所做的更改。

本节包括下列主题：

[Windows Server 2008 和 Windows Vista SP1 的 WHEA 更改](whea-changes-for-windows-server-2008-and-windows-vista-sp1.md)

[Windows 7 的 WHEA 更改](whea-changes-for-windows-7.md)

## <a name="new-whea-changes-for-windows8"></a>Windows 8 的 (*新* 的) WHEA 更改


从 Windows 8 开始，对 Windows 硬件错误体系结构进行了以下更改 (WHEA) 

-   新的 WMI 提供程序类 [**WHEAPolicyManagementMethods**](/windows-hardware/drivers/ddi/_whea/)。
-   可以通过 [**WHEAPolicyManagementMethods**](/windows-hardware/drivers/ddi/_whea/) 或通过 WHEA Powershell 模块管理 WHEA 策略。 如果通过上述任一模式更新策略，策略值将立即生效。
-   不推荐使用 WHEA WMI Method [**WHEAErrorSourceMethods：： SetErrorSourceInfoRtn**](/windows-hardware/drivers/ddi/_whea/) 。

 

