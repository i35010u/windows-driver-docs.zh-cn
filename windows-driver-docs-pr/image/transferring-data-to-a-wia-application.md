---
title: 将数据传输到 WIA 应用程序
description: 将数据传输到 WIA 应用程序
ms.assetid: 3ad906c9-968f-43d7-ae17-fc570440883d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce9fa08a1a51afc1ae8d3ac9c8c4b0e207f5c368
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542291"
---
# <a name="transferring-data-to-a-wia-application"></a>将数据传输到 WIA 应用程序





当应用程序启动数据传输时，WIA 服务调用[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)方法执行传输。 此方法负责获取设备中的数据和发送数据返回到应用程序中使用[ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff543946)方法。

在 Microsoft Windows Millennium Edition （me） 和 Windows XP 中，WIA 微型驱动程序应该能够处理两种类型的数据传输： 文件和内存。 若要确定哪种类型的传输应用程序启动，微型驱动程序应阅读[ **WIA\_IPA\_TYMED** ](https://msdn.microsoft.com/library/windows/hardware/ff551656)属性值或检查**tymed**的成员[ **MINIDRV\_传输\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff545250)结构。 第二个选项是 WIA 微型驱动程序调用才有效[ **wiasGetImageInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549249)第一次服务函数。 **WiasGetImageInformation**服务函数会自动读取 WIA\_IPA\_TYMED 属性和该值赋给**tymed** MINIDRV成员\_传输\_上下文结构。

首选的方法是为 WIA 微型驱动程序可以读取 WIA\_IPA\_TYMED 属性值。 这可以保证微型驱动程序正在执行的获取适当的类型。

从 Windows Vista 开始，引入了一个简化的基于流的传输方法。 有关详细信息，对此数据传输方法请参阅[IStream 数据传输](istream-data-transfers.md)。

本部分介绍以下主题：

[了解 TYMED](understanding-tymed.md)

[为数据分配内存](allocating-memory-for-data.md)

[取消数据传输](canceling-a-data-transfer.md)

[取消挂起的 I/O 操作](canceling-pending-i-o-operations.md)

[原始格式的数据传输](raw-format-data-transfer.md)

有关使用 TYMED （内存中和文件传输） 传输的数据有关的基本信息和基于流的传输请参阅[数据传输](data-transfers.md)。

 

 




