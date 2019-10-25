---
title: 正确使用指向 HwScsiFindAdapter 的 HwContext 指针
description: 正确使用指向 HwScsiFindAdapter 的 HwContext 指针
ms.assetid: 9f287989-423b-4084-bf18-8df8676f7123
keywords:
- SCSI 微型端口驱动程序 WDK 存储，PnP
- PnP WDK SCSI
- 即插即用 WDK SCSI
- 转换 SCSI 微型端口驱动程序
- HwContext 指针
- HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 213c4150ce5f5ebce61e56993711891781804ed9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840328"
---
# <a name="use-the-hwcontext-pointer-to-hwscsifindadapter-correctly"></a>正确使用指向 HwScsiFindAdapter 的 HwContext 指针


## <span id="ddk_use_the_hwcontext_pointer_to_hwscsifindadapter_correctly_kg"></span><span id="DDK_USE_THE_HWCONTEXT_POINTER_TO_HWSCSIFINDADAPTER_CORRECTLY_KG"></span>


如果微型端口驱动程序的[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))从端口驱动程序接收非零访问范围值，则它不能使用*HwContext*指针。 尽管此限制还适用于版本4.0 的微型端口驱动程序，但没有任何内容会阻止此类小型端口驱动程序使用此指针。

如果可将微型端口驱动程序初始化为 Microsoft Windows 2000 和更高版本中的即插即用驱动程序，则它不能使用*HwContext*指针，因为 SCSI 端口驱动程序将作为*HwContext*参数传入**NULL**指针。

必须修改现有微型端口驱动程序的方式取决于当前使用*HwContext*的方式。 例如，如果微型端口驱动程序使用*HwContext*来维护 hba 计数（例如，在**DebugPrint**语句中使用），另一种方法可能是使用*HwDeviceExtension*指针。 *HwDeviceExtension*提供了一个唯一的编号，与发起**DebugPrint**消息的特定 HBA 相关。 （使用全局变量存储 HBA 计数是一种不好的做法，因为微型端口驱动程序不应使用全局变量来维护状态信息。）

再举一个例子，如果4.0 版微型端口驱动程序使用*HwContext*来传达有关要初始化的设备类型的信息（例如，有关 PCI HBA 特定型号支持的功能的信息），则5.0 版本的微型端口驱动程序可以使用[**ScsiPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetbusdata)获取 HBA 的标识符，然后使用该标识符在此类参数块列表中搜索以查找正确的信息。

另一种可能的微型端口驱动程序修改可能是在*ArgumentString*参数传递的注册表字符串中提供此信息。 在初始化期间，可通过微型端口驱动程序的 INF 文件设置注册表字符串，以了解与检测到的卡型号有关的信息。 这比在微型端口驱动程序中硬编码参数提供的灵活性更高，因为这种微型端口驱动程序可以使用更新的 INF 文件处理新型号的卡，而无需重新编译微型端口驱动程序。

 

 




