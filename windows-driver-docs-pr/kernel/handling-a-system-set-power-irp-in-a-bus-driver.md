---
title: 处理总线驱动程序中的系统 Set-Power IRP
description: 处理总线驱动程序中的系统 Set-Power IRP
ms.assetid: e88344bd-4223-4cd5-9428-201d46c6dbb4
keywords:
- 设置电源 Irp WDK 电源管理
- 总线驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e37faf79a6a14a03a95933b60c99bc0c09d58ac6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838677"
---
# <a name="handling-a-system-set-power-irp-in-a-bus-driver"></a>处理总线驱动程序中的系统 Set-Power IRP





当总线驱动程序收到系统设置-power IRP 时，它必须执行以下步骤：

1.  调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)以启动下一个 power IRP。 （仅限 windows Server 2003、Windows XP 和 Windows 2000。）

2.  将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS。 驱动程序无法通过系统设置-power IRP 来失败。

3.  调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)，指定 IO\_NO\_递增，以完成 IRP。

总线驱动程序在收到请求设备电源状态的电源 IRP 之前，不会更改设备电源设置。

 

 




