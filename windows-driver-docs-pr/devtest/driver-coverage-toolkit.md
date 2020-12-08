---
title: 驱动程序覆盖范围工具包
description: 驱动程序覆盖率工具包监视和报告各种 i/o 请求数据包 (Irp) 为指定设备进入或离开驱动程序堆栈。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 201e611912d53773c51be59f42c8e5a662774d41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839007"
---
# <a name="driver-coverage-toolkit"></a>驱动程序覆盖范围工具包


驱动程序覆盖率工具包监视和报告各种 i/o 请求数据包 (Irp) 为指定设备进入或离开驱动程序堆栈。 驱动程序覆盖套件中的数据可帮助确定驱动程序测试和验证期间的覆盖漏洞。

**注意**  Windows 10 不再需要驱动程序覆盖率工具包，并且 WDK 中不再包括该安装程序。 若要在 Windows 10 中执行此处所述的任务，请改用 [驱动程序验证程序](driver-verifier.md) 和 [IRP 日志记录](irp-logging.md)。

 

驱动程序覆盖套件包含在 Windows 驱动程序工具包 (WDK) 中，并从 Visual Studio 运行，作为 [设备基础测试](device-fundamentals-tests.md)的一部分。

驱动程序覆盖套件包含以下工具：

-   [驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md) ( # A0) ，用于监视一个或多个指定设备对驱动程序堆栈的 IRP 请求。

-   驱动程序覆盖工具在 [设备基础测试](device-fundamentals-tests.md)中提供，请参阅 [覆盖率测试 (设备基础) ](coverage-tests--device-fundamentals-.md)。 您可以使用这些工具在指定的设备上启用或禁用 IRP 覆盖区，并从覆盖面数据生成报表。

您可以在测试计算机上安装并运行驱动程序覆盖套件，而不会产生很大影响。 这些工具不会修改 IRP 请求，也不会将其他 Irp 注入到设备的驱动程序堆栈中。 这些工具只收集进入或离开设备驱动程序的每个 IRP 上的数据。

在运行 Windows Vista 和更高版本的 Windows 的系统上支持驱动程序覆盖套件。

本节包含下列主题：

[驱动程序覆盖范围工具包概述](overview-of-the-driver-coverage-toolkit.md)

[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)

[如何收集 IRP 覆盖范围数据](how-to-collect-irp-coverage-data.md)

[如何分析 IRP 覆盖范围数据](how-to-analyze-irp-coverage-data.md)

 

 





