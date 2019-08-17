---
title: 传输微型驱动程序概述
description: 本部分包含需要创建自己的 HID 微型驱动程序的供应商的详细信息。
ms.assetid: 5142A2C9-AE6E-4CE6-AF16-2CF811D6C10F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fa7111302fe827a9b7ba0c3a7850a5f2eccc6ee
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565631"
---
# <a name="transport-minidriver-overview"></a>传输微型驱动程序概述

本部分包含需要创建自己的 HID 微型驱动程序的供应商的详细信息。 如果你的设备需要 USB, 蓝牙, 蓝牙 LE, I i2c, GPIO 作为传输, 请使用 Microsoft 提供的内置驱动程序。 若要查看内置传输微型驱动程序列表, 请参阅[**HID**](hid-transports.md)传输。

对于其他传输, 你将需要写入传输微型驱动程序。

可以使用以下框架之一编写 HID 微型驱动程序:

1.  UMDF –用户模式驱动程序框架
2.  KMDF –内核模式驱动程序框架
3.  WDM –旧 Windows 驱动模型

**请注意**  , Microsoft 鼓励硬件供应商尽可能使用机箱内传输微型驱动程序。 但是, 如果你的设备需要不受支持的传输, Microsoft 建议使用 Windows 驱动程序框架 (UMDF 或 KMDF) 作为微型驱动程序的驱动程序模型。 仅当 Windows 驱动程序框架不支持特定传输时, 才应创建 WDM 微型驱动程序。

Microsoft 建议开发人员使用 UMDF 框架作为起点。 仅当功能不可用于 UMDF 时, 请考虑编写 KMDF 驱动程序。 有关这两个驱动程序框架中的功能比较的信息, 请参阅将 UMDF 2 功能与 KMDF 进行比较。

下表捕获了与 HID 传输微型驱动程序相关的两个 WDF 模型相关的主要优点和挑战。

|            |                                                                                                                  |                                                                                                                               |
|------------|------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
|            | KMDF                                                                                                             | UMDF                                                                                                                          |
| 优点 | 支持所有键盘和鼠标筛选器驱动程序所需的 WDF 的所有 Windows 平台中都提供支持。 | 对于此驱动程序中的大多数垂直设备类错误, 更易于开发和推荐此类错误, 请检查整个系统。 有关详细信息, 请参阅[**编写 UMDF 驱动程序的优点**](../wdf/advantages-of-writing-umdf-drivers.md)。   |
| 难题 | 编写不当的 KDMF HID 传输微型驱动程序会损坏系统。                                              | Windows 8 之前的 Windows 版本不支持 UMDF HID 传输微型驱动程序。 UMDF 驱动程序可以接收来自内核模式驱动程序的 i/o 请求。 这些转换可能会对性能产生轻微影响。 |


## <a name="see-also"></a>请参阅
[**带有 UMDF 的入门**](../wdf/getting-started-with-umdf-version-2.md) 


 




