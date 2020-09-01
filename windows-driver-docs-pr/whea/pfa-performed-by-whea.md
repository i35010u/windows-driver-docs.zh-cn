---
title: 由 WHEA 执行的 PFA
description: 由 WHEA 执行的 PFA
ms.assetid: c93b15aa-9b99-4dfa-8c97-b503654e44f2
keywords:
- 预测性故障分析 (PFA) WDK WHEA，纠错代码内存
- PFA WDK WHEA，纠错代码内存
- 错误更正代码内存 WDK WHEA
- 错误更正代码内存 WDK WHEA、预测性故障分析
- 低级别硬件错误处理程序 WDK WHEA
- LLHEH WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 120f1649f0c297222d1e6cc91a1f9b0837d894b1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208405"
---
# <a name="pfa-performed-by-whea"></a>由 WHEA 执行的 PFA


从 Windows 7 开始，Windows 硬件错误体系结构 (WHEA) 支持预测性故障分析 (PFA) 用于错误纠正代码 (ECC) 内存。

**重要提示**   [ (PSHED) 插件的特定于平台的硬件错误驱动程序](platform-specific-hardware-error-driver-plug-ins2.md)可以在 ECC 内存而不是 WHEA 上执行 PFA。 如果插件执行 PFA，则必须按照 [PSHED 插件执行 PFA](pfa-performed-by-a-pshed-plug-in.md)中所述的步骤进行操作。 插件不得遵循本主题中描述的步骤。

 

出现 ECC 内存错误时，WHEA 执行以下步骤：

1.   (*LLHEH*) 的*低级硬件错误处理程序*将收到有关内存错误情况的通知。

2.  LLHEH 检索错误源中的内存错误信息，并使用错误数据填充硬件错误数据包。 此数据包的格式为 [WHEA \_ 错误 \_ 数据包](/previous-versions/windows/hardware/drivers/ff560465(v=vs.85)) 结构。

3.  LLHEH 调用 PSHED 来检索任何特定于平台的硬件错误信息。 如果已安装并注册了 PSHED 插件来检索有关错误的信息，则 PSHED 将调入 PSHED 插件，以便插件可以修改返回到 LLHEH 的错误信息。

4.  LLHEH 调用 Windows 操作系统内核，并向其传递错误数据包。

5.  Windows 内核创建 [错误记录](error-records.md) ，并向其添加从 LLHEH 收到的错误数据包中的信息。 此外，Windows 内核还添加了有关错误的其他信息 (如错误源、错误的严重性以及错误发生多少次) 错误记录。

6.  Windows 内核调入 PSHED，以允许 PSHED 向错误记录中添加部分。

7.  如果安装了 PSHED 插件并注册了以检索有关错误的信息，则 PSHED 将调入 PSHED 插件，以便插件可以修改错误记录中的信息。

    **注意**   如果 PSHED 插件未执行 PFA，则它不能在[WHEA \_ 错误 \_ 数据包](/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))结构的[**WHEA \_ 错误 \_ 数据包 \_ 标志**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)成员中设置**PlatformPfaControl**位。

     

8.  如果启用了 PFA，则 WHEA 将在 ECC 内存页上执行 PFA。 有关此过程的详细信息，请参阅 [WHEA 如何在 ECC 内存上执行 PFA](how-whea-performs-pfa-on-ecc-memory.md)。

9.  Windows 内核生成 ETW 事件，并在系统事件日志中记录错误消息。

 

