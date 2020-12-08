---
title: 再次设置并从 HwScsiFindAdapter 返回
description: 再次设置并从 HwScsiFindAdapter 返回
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储，HwScsiFindAdapter
- 再次 WDK SCSI
- 返回值 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b59144f9125d2015249133f4b8d0a34a6659de30
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817975"
---
# <a name="setting-again-and-returning-from-hwscsifindadapter"></a>再次设置并从 HwScsiFindAdapter 返回


## <span id="ddk_setting_again_and_returning_from_hwscsifindadapter_kg"></span><span id="DDK_SETTING_AGAIN_AND_RETURNING_FROM_HWSCSIFINDADAPTER_KG"></span>


对于支持且已成功配置的 HBA， [*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 返回 \_ 找到的 SP 返回 \_ 。

在返回之前，应 *再次* 设置旧版和即插即用微型端口驱动程序的 *HwScsiFindAdapter* ，如本部分中所述。 当将微型端口驱动程序作为即插即用驱动程序加载时，这种情况 *同样* 不相关，因此必须对其进行 *适当的设置* ，以便系统可以根据需要将即插即用微型端口驱动程序作为旧驱动程序运行。

*HwScsiFindAdapter* 应 *再次* 设置为 **TRUE** ，以指示应 *使用完全相同的端口配置信息再次调用它，但如果它的另一个 hba 可能连接在同一 i/o 总线上，则使用 \_ 新的 \_ 设备扩展* 。

如果 *HwScsiFindAdapter* 找不到它支持的 HBA，应 *再次* 将其设置为 **FALSE** ，并返回 " \_ 未找到 SP 返回" \_ \_ 。 如果 *HwScsiFindAdapter* 发现支持的 HBA，但输入 [**端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information) 中的配置数据不一致 (如 EISA 总线) 上的无效 **DmaChannel** 或 **BusInterruptLevel** ，则它应 *再次* 设置为 **FALSE** 并返回 SP \_ 返回 \_ 错误 \_ 配置。 对于 PCI 总线上的 HBA， *HwScsiFindAdapter* 必须接受系统提供的中断配置信息。

请注意， *再次* 将设置为 **FALSE** 并返回具有 sp 返回的控制， \_ \_ \_ 或者 sp \_ 返回 \_ 错误的 \_ 配置表明，由输入端口配置信息中的 **SystemIoBusNumber** 标识的给定 i/o \_ 总线 \_ 没有微型端口驱动程序可以支持的 HBA。 它不会阻止系统端口驱动程序再次调用 *HwScsiFindAdapter* ，并提供更新的端口 \_ 配置 \_ 信息来扫描另一个 i/o 总线，以便 (s) 如果计算机具有相同 **AdapterInterfaceType** 的其他 i/o 总线。

 

