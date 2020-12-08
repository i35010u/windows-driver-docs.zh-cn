---
title: PTP 错误恢复
description: PTP 错误恢复
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df7fb15c9a71df64d763edd9cab6b110cf316b9f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829599"
---
# <a name="ptp-error-recovery"></a>PTP 错误恢复





在初始化 Microsoft PTP 类 (微型驱动程序的过程中，初始检索 DeviceInfo 和 ObjectInfo 数据集以及属性说明) 时，任何错误都被视为灾难性故障，WIA 微型驱动程序无法初始化。

在稍后处理 (例如，检索图像时) ，当发生无法识别的错误时，Microsoft PTP 微型驱动程序将首先尝试发送 "获取设备状态" 特定于 USB 类的请求 (如 USB 静止映像捕获设备定义) 中所述。 如果该请求成功，驱动程序将清除所有停止的终结点，并继续。

如果 "获取设备状态" 请求失败，则 PTP 微型驱动程序会尝试使用 USB 静止图像捕获设备定义) 中描述的设备重置类特定 (请求来重置设备。 如果设备重置类特定的请求成功，则返回 S \_ FALSE 而不是 \_ "正常"。 如果重置设备失败，则设备重置类特定的请求将返回错误代码。

 

 




