---
title: 选项文件字段
description: 选项文件字段
ms.assetid: 5ca79c91-5d19-4393-aa5e-be3d47e62967
keywords:
- 选项文件 WDK Static Driver Verifier
- 字段 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 045168ae1a1e38d8a591937e6ef66aa45aa0aedb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356340"
---
# <a name="option-file-fields"></a>选项文件字段


SDV 选项文件包含的 SDV 设置。 一些您可以更改这些设置。 SDV 保留其他设置。

您可以更改选项文件中的字段包括：

<span id="SDV_SlamConfig_Maximum_Driver_Size"></span><span id="sdv_slamconfig_maximum_driver_size"></span><span id="SDV_SLAMCONFIG_MAXIMUM_DRIVER_SIZE"></span>**SDV\_SlamConfig\_Maximum\_Driver\_Size**  
指定 SDV 将支持 （在方面的代码行） 的驱动程序的最大大小。 默认值为 10 万行代码。

<span id="SDV_SlamConfig_Timeout"></span><span id="sdv_slamconfig_timeout"></span><span id="SDV_SLAMCONFIG_TIMEOUT"></span>**SDV\_SlamConfig\_Timeout**  
限制 SDV 可以验证每个规则所花费的时间。 此项的值是一个整数，表示的秒数。 最小值为 10，最大值是 86400，默认值为 3000 （50 分钟为单位）。

如果验证规则时，SDV 超过每个规则的时间限制，终止的验证和报告**超时**中[命令行输出](command-line-output.md)和中上的结果部分下的 Static Driver Verifier**Main**选项卡。

<span id="SDV_SlamConfig_Spaceout"></span><span id="sdv_slamconfig_spaceout"></span><span id="SDV_SLAMCONFIG_SPACEOUT"></span>**SDV\_SlamConfig\_Spaceout**  
限制 SDV 验证每个规则时可以使用的虚拟内存的量。 此项的值是以兆字节 (MB) 为单位的整数。 最小值为 100，并且默认值为 2500 MB (2.5 GB)。

SDV 超出了验证规则时的虚拟内存限制，终止的验证和报告**Spaceout**中[命令行输出](command-line-output.md)并在结果部分下的 Static Driver Verifier上**Main**选项卡。

如果报告了 SDV **Spaceout**，请考虑增加的值**SDV\_SlamConfig\_Spaceout**，SDV 正在运行，或移动时在计算机上停止所有其他进程SDV 到具有更多内存的计算机。 系统的最佳值为大约 200 MB 小于在系统上的物理内存量。

<span id="SDV_SlamConfig_NumberOfThreads"></span><span id="sdv_slamconfig_numberofthreads"></span><span id="SDV_SLAMCONFIG_NUMBEROFTHREADS"></span>**SDV\_SlamConfig\_NumberOfThreads**  
设置要在验证过程中使用线程的数。 如果值为 0，这将限制 （这包括超线程处理器） 的计算机上的处理器数量的线程数。 如果值设置为一个数字大于 0，则值将指定 SDV 可以验证时使用的线程的数。 增加线程数可能会增加运行的时性能的 SDV，但它还可能增加超时发生数。 默认值为 0。 如果使用的默认值的多处理器计算机上正在运行 SDV，SDV 自动将充分利用额外的处理器。

 

 





