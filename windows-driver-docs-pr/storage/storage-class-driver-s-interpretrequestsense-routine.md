---
title: 存储类驱动程序的 InterpretRequestSense 例程
description: 存储类驱动程序的 InterpretRequestSense 例程
keywords:
- InterpretRequestSense
- 请求感知 WDK 存储
- 错误 WDK 存储
- 正在重试 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 136f2a62da71eb9e100f8c62be649d1941dedcb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794197"
---
# <a name="storage-class-drivers-interpretrequestsense-routine"></a>存储类驱动程序的 InterpretRequestSense 例程


## <span id="ddk_storage_class_drivers_interpretrequestsense_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_INTERPRETREQUESTSENSE_ROUTINE_KG"></span>


*InterpretRequestSense* 例程解释在 SRB 的 **SenseInfoBuffer** 中返回的数据，确定是否应重试该请求，如果不是，则将该错误映射到 IRP 的 I/O 状态块的 NTSTATUS 值。

系统端口驱动程序指示是否可以通过 \_ 在 SrbStatus 中设置 SRB 状态 "自动 \_ 感知 \_ \_ \_ " "有效" 或 "SRB 状态请求 \_ \_ "。 **SrbStatus**

如果没有可用的请求感知信息， *InterpretRequestSense* 应检查 **SrbStatus** 值以确定是重试给定请求还是确定到 NTSTATUS 值的相应映射。

*InterpretRequestSense* 例程也可能调用驱动程序提供的错误日志记录例程。 每当存储类驱动程序记录 i/o 错误时，它应包含由 SRB 中的存储端口驱动程序设置的 **PathId**、 **TargetId**、 **Lun** 和 **SrbStatus** 值，并在可能的情况下包括作为错误日志条目 **DumpData** 一部分的相关请求感知信息。 请注意，存储类驱动程序不得使用此类 SRBs 中的 **PathId**、 **TargetId** 和 **Lun** 来处理其他请求。

有关记录 i/o 错误的详细信息，请参阅 [日志记录错误](../kernel/logging-errors.md)。

 

