---
title: 正确使用 HwContext 指向 HwScsiFindAdapter
description: 正确使用 HwContext 指向 HwScsiFindAdapter
ms.assetid: 9f287989-423b-4084-bf18-8df8676f7123
keywords:
- SCSI 微型端口驱动程序 WDK 存储，即插即用
- 即插即用 WDK SCSI
- Plug and Play WDK SCSI
- 转换 SCSI 微型端口驱动程序
- HwContext 指针
- HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20fb54b6db08f04b7e2087f83392fb9cf30680df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521813"
---
# <a name="use-the-hwcontext-pointer-to-hwscsifindadapter-correctly"></a>正确使用 HwContext 指向 HwScsiFindAdapter


## <span id="ddk_use_the_hwcontext_pointer_to_hwscsifindadapter_correctly_kg"></span><span id="DDK_USE_THE_HWCONTEXT_POINTER_TO_HWSCSIFINDADAPTER_CORRECTLY_KG"></span>


如果微型端口驱动程序[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)接收非零值的访问范围值从端口驱动程序，它必须使用*HwContext*指针。 尽管此限制也应用于版本 4.0 的微型端口驱动程序，执行任何操作阻止这样的微型端口驱动程序使用此指针。

如果可以作为插驱动程序在 Microsoft Windows 2000 及更高版本初始化微型端口驱动程序，它必须使用*HwContext*指针因为 SCSI 端口驱动程序传入**NULL**作为指针*HwContext*参数。

必须修改现有的微型端口驱动程序的方式取决于它当前使用的方式*HwContext*。 例如，如果微型端口驱动程序将使用*HwContext*维护 Hba 的计数 (例如，若要在中使用**DebugPrint**语句) 是一种替代方法使用*HwDeviceExtension*指针相反。 *HwDeviceExtension*提供了与特定 HBA 相关的唯一编号发起**DebugPrint**消息。 （使用全局变量来存储 HBA 计数是个好办法，因为微型端口驱动程序不应使用全局变量来维护状态信息。）

再举一例，如果微型端口驱动程序 4.0 版本使用*HwContext*进行通信的设备正在初始化 （如 PCI HBA 的特定模型支持的功能有关的信息类型有关的信息)，可能会使用微型端口驱动程序的 5.0 版本[ **ScsiPortGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff564624)若要获取 HBA 标识符，然后使用该标识符来搜索此类参数块以查找正确的列表信息。

另一种可能的微型端口驱动程序修改可能是提供此信息的注册表字符串中传入*ArgumentString*参数。 在检测到的卡片的模型与相关的信息的初始化过程中，可以将注册表字符串的微型端口驱动程序的 INF 文件设置。 这提供了更大的灵活性比硬编码微型端口驱动程序中的参数因为这样的微型端口驱动程序无法处理新模型的卡而无需重新编译的微型端口驱动程序使用更新的 INF 文件。

 

 




