---
title: 传输微型驱动程序
description: 本部分包含的供应商需要创建其自己的 HID 微型驱动程序的详细信息。
ms.assetid: 5142A2C9-AE6E-4CE6-AF16-2CF811D6C10F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c258c97b28fdf095d604cbbc74e090135ec044b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567272"
---
# <a name="transport-minidrivers"></a>传输微型驱动程序


本部分包含的供应商需要创建其自己的 HID 微型驱动程序的详细信息。 如果你的设备需要 USB、 蓝牙、 蓝牙 LE、 I²C、 GPIO 作为传输协议，使用由 Microsoft 提供的现成驱动程序。 若要查看的现成传输微型驱动程序的列表，请参阅[ **HID 传输**](hid-transports.md)。

对于其他传输，需要编写传输微型驱动程序。

HID 微型驱动程序可以通过使用以下框架之一编写：

1.  UMDF – 用户模式驱动程序框架
2.  KMDF – 内核模式驱动程序框架
3.  WDM – 旧版 Windows 驱动程序模型

**请注意**  Microsoft 鼓励硬件供应商使用机箱中传输的微型驱动程序只要有可能。 但是，如果你的设备需要不受支持的传输，Microsoft 建议使用 Windows 驱动程序框架 （UMDF 或 KMDF） 的驱动程序模型作为你微型驱动程序。 如果在特定的传输协议不受 Windows 驱动程序框架，您只应创建 WDM 微型驱动程序。

Microsoft 建议开发人员使用 UMDF framework 作为起始点。 仅当功能不供 UMDF，应考虑编写 KMDF 驱动程序。 有关功能比较两个驱动程序框架中的信息，请参阅将 UMDF 2 功能比较 KMDF。

下表列出了主要优势和挑战，因为它们与 HID 传输微型驱动程序与两个 WDF 模型相关联。

|            |                                                                                                                  |                                                                                                                               |
|------------|------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
|            | KMDF                                                                                                             | UMDF                                                                                                                          |
| 优点 | 支持用于支持 WDF 所需的所有键盘和鼠标的筛选器驱动程序的所有 Windows 平台。 | 更轻松地开发和建议大多数垂直设备类中此驱动程序的错误进行不 bug 检查整个系统。 有关详细信息，请参阅[**优点的编写 UMDF 驱动程序**](../wdf/advantages-of-writing-umdf-drivers.md)。   |
| 难题 | 编写质量差的 KDMF HID 传输微型驱动程序可以使系统崩溃。                                              | UMDF HID 的传输微型驱动程序是不受支持版本的 Windows 8 之前的 Windows。 UMDF 驱动程序可以从内核模式驱动程序接收的 I/O 请求。 这些转换可以略微的性能影响。 |


## <a name="see-also"></a>请参阅
[**开始使用 UMDF**](../wdf/getting-started-with-umdf-version-2.md) 


 




