---
title: 存储类驱动程序的 InterpretRequestSense 例程
description: 存储类驱动程序的 InterpretRequestSense 例程
ms.assetid: abfb529d-7fab-40f7-b4cd-e6adb4cf643e
keywords:
- InterpretRequestSense
- 请求检测 WDK 存储
- 错误 WDK 存储
- 正在重试请求 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92d161689c48d8d8364f0dada691162b14f551d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575159"
---
# <a name="storage-class-drivers-interpretrequestsense-routine"></a>存储类驱动程序的 InterpretRequestSense 例程


## <span id="ddk_storage_class_drivers_interpretrequestsense_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_INTERPRETREQUESTSENSE_ROUTINE_KG"></span>


*InterpretRequestSense*例程将解释在 SRB 中返回的数据**SenseInfoBuffer**，确定是否应重试请求，以及如果不是，将错误映射到的 NTSTATUS 值IRP 的 I/O 状态块。

系统端口驱动程序指示请求检测信息是否可通过设置 SRB\_状态\_自动感知\_VALID 还是 SRB\_状态\_请求\_意义上\_中的失败**SrbStatus**。

如果没有请求检测信息不可用， *InterpretRequestSense*应检查**SrbStatus**值以确定是否重试某个给定的请求，或者想要确定的相应映射到NTSTATUS 值。

*InterpretRequestSense*例程可能会调用一个驱动程序提供错误日志记录例程也。 每当存储类驱动程序日志的 I/O 错误，它应包括**PathId**， **TargetId**， **Lun**，以及**SrbStatus**设置值SRB 中的存储端口驱动程序和，如果可能，作为一部分错误相关的请求检测信息日志条目的**DumpData**。 请注意，不能使用存储类驱动程序**PathId**， **TargetId**，并**Lun**从这种 Srb 解决其他请求。

有关日志记录的 I/O 错误的详细信息，请参阅[日志记录错误](https://msdn.microsoft.com/library/windows/hardware/ff554312)。

 

 




