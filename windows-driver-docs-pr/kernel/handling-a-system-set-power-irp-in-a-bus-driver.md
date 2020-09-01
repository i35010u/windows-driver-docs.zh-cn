---
title: 处理总线驱动程序中的系统 Set-Power IRP
description: 处理总线驱动程序中的系统 Set-Power IRP
ms.assetid: e88344bd-4223-4cd5-9428-201d46c6dbb4
keywords:
- 设置电源 Irp WDK 电源管理
- 总线驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e1fd1fedb06ad446bceefec1f7d18f88a0b410f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190455"
---
# <a name="handling-a-system-set-power-irp-in-a-bus-driver"></a>处理总线驱动程序中的系统 Set-Power IRP





当总线驱动程序收到系统设置-power IRP 时，它必须执行以下步骤：

1.  调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 以启动下一个 power IRP。 仅 (Windows Server 2003、Windows XP 和 Windows 2000。 ) 

2.  将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。 驱动程序无法通过系统设置-power IRP 来失败。

3.  调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)，指定 IO \_ 无 \_ 增量，以完成 IRP。

总线驱动程序在收到请求设备电源状态的电源 IRP 之前，不会更改设备电源设置。

 

