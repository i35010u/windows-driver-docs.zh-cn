---
title: 再次设置并从 HwScsiFindAdapter 返回
description: 再次设置并从 HwScsiFindAdapter 返回
ms.assetid: 8a9cde40-06fa-4b56-818d-63a9c71da208
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储，HwScsiFindAdapter
- 再次 WDK SCSI
- 返回值 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 824f3ec22fb4f79e3ae0bee3019c61d356334e68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845231"
---
# <a name="setting-again-and-returning-from-hwscsifindadapter"></a>再次设置并从 HwScsiFindAdapter 返回


## <span id="ddk_setting_again_and_returning_from_hwscsifindadapter_kg"></span><span id="DDK_SETTING_AGAIN_AND_RETURNING_FROM_HWSCSIFINDADAPTER_KG"></span>


对于支持且已成功配置的 HBA， [*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))返回 SP\_返回\_找到。

在返回之前，应*再次*设置旧版和即插即用微型端口驱动程序的*HwScsiFindAdapter* ，如本部分中所述。 当将微型端口驱动程序作为即插即用驱动程序加载时，这种情况*同样*不相关，因此必须对其进行*适当的设置*，以便系统可以根据需要将即插即用微型端口驱动程序作为旧驱动程序运行。

*HwScsiFindAdapter*应*再次*设置为**TRUE** ，以指示应*使用完全相同的端口再次调用该端口\_配置\_信息，但*如果它的另一个 hba 可能已连接，则为新的设备扩展在同一 i/o 总线上。

如果*HwScsiFindAdapter*找不到它支持的 HBA，则它应*再次*设置为**FALSE**并返回 SP\_返回\_未\_找到。 如果*HwScsiFindAdapter*发现支持的 HBA 但输入[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)具有不一致的配置数据（例如，在 EISA 总线上的**DmaChannel**或**BusInterruptLevel**无效），则应*再次*设置为**FALSE**并返回 SP\_返回\_错误\_配置。 对于 PCI 总线上的 HBA， *HwScsiFindAdapter*必须接受系统提供的中断配置信息。

请注意，*再次*设置为**FALSE**并返回具有 SP\_返回\_未\_找到或 SP\_返回\_错误\_配置指示给定 I/o 总线，由**SystemIoBusNumber**标识在输入端口\_配置\_信息中，无小型端口驱动程序可以支持的 HBA。 它不会阻止系统端口驱动程序再次调用*HwScsiFindAdapter* ，并\_配置\_信息来扫描 HBA 的另一个 i/o 总线，如果计算机具有相同**的其他 i/o 总线AdapterInterfaceType**。

 

 




