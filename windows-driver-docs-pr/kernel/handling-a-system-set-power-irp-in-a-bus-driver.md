---
title: 处理总线驱动程序中的系统 Set-Power IRP
description: 处理总线驱动程序中的系统 Set-Power IRP
ms.assetid: e88344bd-4223-4cd5-9428-201d46c6dbb4
keywords:
- 设置 power Irp WDK 电源管理
- 总线驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 482e495e7806b24659e43b0aeade26094e8b883c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359823"
---
# <a name="handling-a-system-set-power-irp-in-a-bus-driver"></a>处理总线驱动程序中的系统 Set-Power IRP





当总线驱动程序收到一个系统集 power IRP，它必须执行以下步骤：

1.  调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)启动下一个幂 IRP。 （Windows Server 2003、 Windows XP 和 Windows 2000 仅。）

2.  设置**Irp-&gt;IoStatus.Status**于状态\_成功。 该驱动程序不能故障系统集 power IRP。

3.  调用[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)，指定 IO\_否\_增量，以完成 IRP。

总线驱动程序不会更改设备电源设置，直到收到 power IRP 请求设备电源状态。

 

 




