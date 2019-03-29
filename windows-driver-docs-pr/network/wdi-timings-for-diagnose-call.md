---
title: 诊断调用的计时
description: 计时要求的诊断以收集调试信息如下所示。
ms.assetid: A21687FE-1398-4722-89E3-BFB511AA48E3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45cb96f597367a22feb673b10e4843e8e9adbd70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577368"
---
# <a name="timings-for-diagnose-call"></a>诊断调用的计时


计时要求的诊断以收集调试信息如下所示。

在级别**DiagnoseLevelHardwareRegisters**，LE 预期收集设备控制诊断调用的输出缓冲区中注册不超过 1 KB。 这是正常发布产品的设置。 它旨在用于收集设备控制寄存器的重要信息。 若要收集此类信息的时间限制是为 25 ms。

在级别**DiagnoseLevelFirmwareImageDump**或**DiagnoseLevelDriverStateDump**，LE 预期收集设备控制寄存器和固件完全转储。 如果时间允许，LE 还可以收集的驱动程序状态，受时间限制。 除了控制寄存器中诊断收集输出的缓冲区、 固件转储和驱动程序状态应保存到文件使用所选的名称在 %windir%\\system32\\驱动程序。 若要收集在任一级别的所有调试信息的时间应在 25 秒内。 这些诊断级别为了在自承载阶段使用。

## <a name="related-topics"></a>相关主题


[**eDiagnoseLevel**](https://msdn.microsoft.com/library/windows/hardware/mt297626)

[*MiniportWdiAdapterHangDiagnose*](https://msdn.microsoft.com/library/windows/hardware/mt297558)

 

 






