---
title: 使用 WMI 库注册块
description: 使用 WMI 库注册块
ms.assetid: 1f4b773d-ca24-47f5-87e8-84c98dad9267
keywords:
- WMI WDK 内核，向 WMI 注册
- 注册 WMI 数据提供程序
- 数据提供程序 WDK WMI
- 驱动程序注册 WDK WMI
- 事件阻止 WDK WMI
- 块 WDK WMI
- IRP_MN_REGINFO
- IRP_MN_REGINFO_EX
- 注册块
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f343262d5e71fe5c3081920c66fbf21d209ca579
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372231"
---
# <a name="using-the-wmi-library-to-register-blocks"></a>使用 WMI 库注册块





驱动程序可以使用 WMI 库来处理[ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)并[ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734)请求如果它正在注册的块，请勿使用动态实例名称，或使用基于 PDO 或驱动程序定义的基本名称字符串的静态实例名称。 在此情况下，该驱动程序：

1.  调用[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)用一个指针指向驱动程序的设备对象，指向[ **WMILIB\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff565813)结构，以及指向 IRP 的

    **WMILIB\_上下文**结构表示要注册的块的数目 (**GuidCount**) 和点到一系列[ **WMIGUIDREGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff565811)结构 (**GuidList**)，用于指定 GUID 的实例，并适用于相应的块的注册标志数。 它还定义入口点的驱动程序的必需和可选*DpWmiXxx*回调例程。

2.  当 WMI 调用驱动程序的[ *DpWmiQueryReginfo* ](https://msdn.microsoft.com/library/windows/hardware/ff544097)例程，该驱动程序指定驱动程序的注册表路径、 其 MOF 资源名称、 适用于所有其块和信息的注册标志WMI 使用的驱动程序的数据块，它可以是名称实例指向物理设备对象的指针传递给驱动程序的[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程或基于字符串静态实例名称。

驱动程序必须进行初始化的入口点及其*DpWmiXxx*中的回调例程**WMILIB\_上下文**结构之前，调用**WmiSystemControl**，可以推迟的初始化，但**GuidCount**并**GuidList**中**WMILIB\_上下文**结构，直到 WMI 调用驱动程序*DpWmiQueryReginfo*例程。

 

 




