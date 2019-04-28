---
title: 由 WHEA 执行的 PFA
description: 由 WHEA 执行的 PFA
ms.assetid: c93b15aa-9b99-4dfa-8c97-b503654e44f2
keywords:
- 预计故障分析 (PFA) WDK WHEA，错误更正代码内存
- PFA WDK WHEA，错误更正代码内存
- 错误更正代码内存 WDK WHEA
- 错误更正代码内存 WDK WHEA，预计故障分析
- 低级别的硬件错误处理程序 WDK WHEA
- LLHEH WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93c872d0fa9c58e75df5c763fc8a12075383b8e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340735"
---
# <a name="pfa-performed-by-whea"></a>由 WHEA 执行的 PFA


从 Windows 7 开始，Windows 硬件错误体系结构 (WHEA) 支持错误更正代码 (ECC) 内存用于预测故障分析 (PFA)。

**重要**  A[特定于平台的硬件错误驱动程序 (PSHED) 插件](platform-specific-hardware-error-driver-plug-ins2.md)可以执行 PFA ECC 内存而不是 WHEA 上。 如果该插件执行 PFA，它必须遵循中所述的步骤[PFA 由 PSHED 插件](pfa-performed-by-a-pshed-plug-in.md)。 该插件必须遵循本主题中所述的步骤。

 

ECC 内存错误时，WHEA 会执行以下步骤：

1.  *低级别的硬件错误处理程序*(*LLHEH*) 通知的内存错误条件是否存在。

2.  LLHEH 从错误源检索内存错误信息和使用错误数据来填充硬件错误数据包中。 此数据包的格式设置为[WHEA\_错误\_数据包](https://msdn.microsoft.com/library/windows/hardware/ff560465)结构。

3.  若要检索特定于平台的硬件错误的任何信息 PSHED LLHEH 调用。 如果 PSHED 插件中安装并注册要检索有关错误的信息，PSHED 将调入 PSHED 插件，以便该插件可以修改返回给 LLHEH 的错误信息。

4.  LLHEH 调用 Windows 操作系统内核，并向其传递错误数据包。

5.  创建 Windows 内核[错误记录](error-records.md)并向其添加信息从 LLHEH 从接收到的错误数据包。 此外，Windows 内核向有关错误的其他信息 （例如，发生错误源，错误和多少次错误的严重级别） 的错误记录。

6.  Windows 内核调用 PSHED 允许 PSHED 将部分添加到的错误记录。

7.  如果 PSHED 插件安装并注册要检索有关错误的信息，PSHED 将调入 PSHED 插件，以便该插件可以修改的错误记录中的信息。

    **请注意**  PSHED 插件不执行 PFA 时，如果它必须设置**PlatformPfaControl**位[ **WHEA\_错误\_数据包\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff560472)的成员[WHEA\_错误\_数据包](https://msdn.microsoft.com/library/windows/hardware/ff560465)结构。

     

8.  如果启用了 PFA，WHEA 执行 PFA ECC 内存页上。 有关此过程的详细信息，请参阅[如何 WHEA 执行 PFA ECC 内存](how-whea-performs-pfa-on-ecc-memory.md)。

9.  Windows 内核会生成一个 ETW 事件和系统事件日志中记录错误的信息。

 

 




