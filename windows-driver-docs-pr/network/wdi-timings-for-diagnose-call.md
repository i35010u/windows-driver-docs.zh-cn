---
title: 诊断呼叫的计时
description: 诊断收集调试信息的计时要求如下所示。
ms.assetid: A21687FE-1398-4722-89E3-BFB511AA48E3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e185dbe86ef1d335a0ba1aa69d456c3260466a30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842891"
---
# <a name="timings-for-diagnose-call"></a>诊断呼叫的计时


诊断收集调试信息的计时要求如下所示。

在**DiagnoseLevelHardwareRegisters**级别，该 LE 应收集诊断调用的输出缓冲区中不超过1kb 的设备控制寄存器。 这是正常发布产品的设置。 它用于收集设备控制寄存器的重要信息。 收集此类信息的时间限制为25毫秒。

在**DiagnoseLevelFirmwareImageDump**或**DiagnoseLevelDriverStateDump**的级别，LE 应收集设备控制寄存器和固件完整转储。 如果时间允许，则 LE 还可以根据时间限制收集驱动程序状态。 除了诊断输出缓冲区中收集的控制寄存器外，固件转储和驱动程序状态应保存到文件中，并在% windir%\\system32\\驱动程序中选择名称。 在任一级别收集所有调试信息的时间应在25秒内。 应在自承载阶段使用这些诊断级别。

## <a name="related-topics"></a>相关主题


[**eDiagnoseLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-ediagnoselevel)

[*MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)

 

 






