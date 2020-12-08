---
title: 选项文件字段
description: 选项文件字段
keywords:
- 选项文件 WDK 静态驱动程序验证程序
- 字段 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b28062508e6774eab57f2c3090381b5a76df4dd7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840793"
---
# <a name="option-file-fields"></a>选项文件字段


SDV 选项文件包含 SDV 设置。 其中一些设置可以更改。 其他设置由 SDV 保留。

选项文件中可以更改的字段包括以下各项：

<span id="SDV_SlamConfig_Maximum_Driver_Size"></span><span id="sdv_slamconfig_maximum_driver_size"></span><span id="SDV_SLAMCONFIG_MAXIMUM_DRIVER_SIZE"></span>**SDV \_ SlamConfig \_ 最大 \_ 驱动程序 \_ 大小**  
指定 SDV 将支持) 的代码行 (的驱动程序的最大大小。 默认值为100K 的代码行。

<span id="SDV_SlamConfig_Timeout"></span><span id="sdv_slamconfig_timeout"></span><span id="SDV_SLAMCONFIG_TIMEOUT"></span>**SDV \_ SlamConfig \_ 超时**  
限制 SDV 在验证每个规则时可以花费的时间。 此项的值是一个整数，表示秒数。 最小值为10，最大值为86400，默认值为 3000 (50 分钟) 。

如果在验证规则时，SDV 超出每个规则的时间限制，则它会终止验证，并在 [命令行输出](command-line-output.md)和 "**主**" 选项卡上的 "结果" 部分下的 "静态驱动程序验证器" 中报告 **超时**。

<span id="SDV_SlamConfig_Spaceout"></span><span id="sdv_slamconfig_spaceout"></span><span id="SDV_SLAMCONFIG_SPACEOUT"></span>**SDV \_ SlamConfig \_ Spaceout**  
限制 SDV 在验证每个规则时可以使用的虚拟内存量。 此项的值是以兆字节为单位的整数 (MB) 单位。 最小值为100，默认值为 2500 MB (2.5 GB ) 

如果在验证规则时，SDV 超出了虚拟内存限制，则它会终止验证，并在 [命令行输出](command-line-output.md)和 "**主**" 选项卡上的 "结果" 部分下的 "静态驱动程序验证器" 中报告 **Spaceout** 。

如果 SDV 报告 **Spaceout**，请考虑增加 **SDV \_ SlamConfig \_ SPACEOUT** 的值，在 SDV 运行时停止计算机上的所有其他进程，或将 SDV 移动到具有更多内存的计算机。 系统的最佳值约为 200 MB，小于系统的物理内存量。

<span id="SDV_SlamConfig_NumberOfThreads"></span><span id="sdv_slamconfig_numberofthreads"></span><span id="SDV_SLAMCONFIG_NUMBEROFTHREADS"></span>**SDV \_ SlamConfig \_ NumberOfThreads**  
设置要在验证期间使用的线程数。 如果该值为0，则将线程数限制为计算机上的处理器数， (这包括超线程处理器) 。 如果将该值设置为大于0的数字，则该值指定 SDV 在验证期间可以使用的线程数。 增加线程数可能会增加 SDV 的运行时性能，但也可能增加发生超时的次数。 默认值为 0。 如果在使用默认值的多处理器计算机上运行 SDV，则 SDV 将自动利用附加的处理器。

 

 





