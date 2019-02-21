---
title: PTP 错误恢复
description: PTP 错误恢复
ms.assetid: 0f89d6b6-9d95-4e98-aa90-08c9508a2228
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f17076f041998e16e8100aaff94c6bd97cf8957
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545476"
---
# <a name="ptp-error-recovery"></a>PTP 错误恢复





在 Microsoft PTP 类微型驱动程序的初始化过程中 （也就是说，在初始检索的 DeviceInfo 和 ObjectInfo 数据集和属性说明），任何错误都会被视为灾难性故障，而且 WIA 微型驱动程序初始化失败。

更高版本 （例如，检索图像） 时的处理过程中出现无法识别的错误时，Microsoft PTP 微型驱动程序首先尝试发送 （USB 仍映像捕获设备定义中所述） 获取设备状态 USB 类特定于请求. 如果该请求成功，驱动程序将清除任何已停止的终结点，并将继续。

如果获取设备状态请求失败，PTP 微型驱动程序将尝试重置设备使用设备重置特定于类的请求 （USB 仍映像捕获设备定义中所述）。 如果设备重置特定于类的请求成功，它将返回 S\_而不是 S FALSE\_确定。 如果将设备重置失败，设备重置特定于类的请求将返回错误代码。

 

 




