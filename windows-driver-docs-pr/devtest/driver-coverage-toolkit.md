---
title: 驱动程序覆盖范围工具包
description: 驱动程序覆盖范围工具包监视器和各种 I/O 请求数据包 (Irp)，进入或离开指定设备驱动程序堆栈上的报表。
ms.assetid: b35ca87e-9ec7-4e25-89ce-0e7c121f6445
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5facc6b1d8962aad294e99983f4a6372bfd407ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380615"
---
# <a name="driver-coverage-toolkit"></a>驱动程序覆盖范围工具包


驱动程序覆盖范围工具包监视器和各种 I/O 请求数据包 (Irp)，进入或离开指定设备驱动程序堆栈上的报表。 该驱动程序覆盖范围工具包中的数据可帮助标识驱动程序测试和验证过程中的覆盖率的弱点。

**请注意**  的驱动程序覆盖范围工具包不再需要在 Windows 10 中，安装程序不再包含在 WDK 中。 若要执行此处所述在 Windows 10 中的任务，请改用[Driver Verifier](driver-verifier.md)并[IRP 日志记录](irp-logging.md)。

 

驱动程序覆盖范围工具包包含 Windows Driver Kit (WDK) 中，从 Visual Studio 运行作为的一部分[设备基础测试](device-fundamentals-tests.md)。

驱动程序覆盖范围工具包包括以下工具：

-   [驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)(Drvcov.sys)，它会监视 IRP 请求执行和跳出执行一个或多个指定设备驱动程序堆栈。

-   驱动程序覆盖工具都可用作的一部分[设备基础测试](device-fundamentals-tests.md)，请参阅[覆盖率测试 （设备基础）](coverage-tests--device-fundamentals-.md)。 这些工具可用于启用或禁用指定设备上的 IRP 覆盖，以及生成报表从覆盖率数据。

可以安装并无大影响的测试计算机上运行的驱动程序覆盖范围工具包。 这些工具不会修改 IRP 请求或将其他 Irp 注入到设备的驱动程序堆栈。 这些工具只需在每个 IRP 的进入或离开设备驱动程序上收集数据。

在运行 Windows Vista 和更高版本的 Windows 的系统上支持的驱动程序覆盖范围工具包。

本部分包含以下主题：

[驱动程序覆盖范围 Toolkit 概述](overview-of-the-driver-coverage-toolkit.md)

[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)

[如何收集 IRP 覆盖率数据](how-to-collect-irp-coverage-data.md)

[如何分析 IRP 覆盖率数据](how-to-analyze-irp-coverage-data.md)

 

 





