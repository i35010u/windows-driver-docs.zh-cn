---
title: 再次设置并从 HwScsiFindAdapter 返回
description: 再次设置并从 HwScsiFindAdapter 返回
ms.assetid: 8a9cde40-06fa-4b56-818d-63a9c71da208
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储 HwScsiFindAdapter
- 再次 WDK SCSI
- 返回值 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5e5294d49243fe708b76837135ac9f5b647133
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341241"
---
# <a name="setting-again-and-returning-from-hwscsifindadapter"></a>再次设置并从 HwScsiFindAdapter 返回


## <span id="ddk_setting_again_and_returning_from_hwscsifindadapter_kg"></span><span id="DDK_SETTING_AGAIN_AND_RETURNING_FROM_HWSCSIFINDADAPTER_KG"></span>


对于支持的和已成功配置 HBA 中， [ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)返回 SP\_返回\_找到。

它将返回之前，请*HwScsiFindAdapter*微型端口驱动程序应设置的旧版和插*Again*在本部分中所述。 尽管*Again*微型端口驱动程序加载作为插驱动程序时不起作用*Again*必须正确设置，以便系统可以运行插微型端口驱动程序作为旧驱动程序如有必要.

*HwScsiFindAdapter*应设置*Again*到**TRUE**以指示它应再次调用*完全相同的端口与\_配置\_信息，但新设备扩展*如果另一个其 Hba 可能连接相同的 I/O 总线上。

如果*HwScsiFindAdapter*找不到 HBA 它支持，但它应设置*Again*到**FALSE** ，并返回 SP\_返回\_不\_找到。 如果*HwScsiFindAdapter*查找受支持的 HBA，但输入[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff563900)具有不一致的配置数据 (如无效**DmaChannel**或**BusInterruptLevel** EISA 总线上)，应设置*Again*到**FALSE**和返回 SP\_返回\_错误\_配置。 有关在 PCI 总线上的 HBA *HwScsiFindAdapter*必须接受由系统提供的中断配置信息。

请注意，设置*Again*到**FALSE**并返回具有 SP 控件\_返回\_不\_找到或 SP\_返回\_坏\_配置指示给定的 I/O 总线，标识由**SystemIoBusNumber**中输入端口\_配置\_的信息，有的微型端口驱动程序可以支持任何 HBA。 它不会阻止系统端口驱动程序调用*HwScsiFindAdapter*再次通过更新端口\_配置\_HBA(s) 扫描另一个 I/O 总线，如果计算机上存在其他 I/O 总线的信息相同**AdapterInterfaceType**。

 

 




