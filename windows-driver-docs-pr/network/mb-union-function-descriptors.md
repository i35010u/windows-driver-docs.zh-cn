---
title: MB 联合功能描述符
description: 本部分介绍联合功能描述符和 MBIM 向后兼容的 MB 设备的新功能
ms.assetid: 4B8C63DD-4B8D-40AB-A6DF-0466343E7E45
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeb663a4eacb06832dcca998838a85d770651b38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374035"
---
# <a name="mb-union-function-descriptors"></a>MB 联合功能描述符


## <a name="union-function-descriptors"></a>联合功能描述符


实现 Ufd 的移动宽带设备具有设备类 / 子类 / 协议的 2 / 0 / 0 作为设备所需的 CDC。 这会阻止 Windows 设备上加载 USBCCGP。 有关 Windows 如何加载 USBCCGP 复合设备上的信息，请参阅[USB 通用父驱动程序 (Usbccgp.sys)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

若要允许 Windows 加载 USBCCGP，设备需要报告的 Microsoft 操作系统兼容 ID 为"CDC\_WMC"未配置设备时。 检测的兼容 ID 后"CDC\_WMC"，Windows 加载 USBCCGP，并 USBCCGP 1 到设备上设置的配置。 USBCCGP 然后将再次查询的 Microsoft 操作系统兼容 Id 中。 但是，设备应报告的 Microsoft 操作系统兼容 ID 时这一次，"CDC\_WMC"。 设备可能会报告 Microsoft 操作系统兼容 Id 中所选的配置函数。

![如果未配置设备的 microsoft os 描述符的 usbhub 查询](images/mbim1.png)

如果未配置设备的 Microsoft 操作系统描述符的 USBHUB 查询

![设备响应 cdc\-wmc，这会导致 windows 加载 usbccgp。](images/mbim2.png)

使用设备做出响应"CDC\_WMC"，这将导致 Windows 加载 USBCCGP

![usbccgp 选择配置\#在设备上的 1。](images/mbim3.png)

USBCCGP 选择配置\#在设备上的 1。

![设备选择配置，并采用兼容 id 列表。](images/mbim4.png)

设备选择配置，并采用兼容 Id 列表。 设备可能包括 CompatID2，这是必需的 Function2。

![在加载后，usbccgp 查询 microsoft 操作系统兼容 id 试。](images/mbim5.png)

在加载后，USBCCGP 查询 Microsoft 操作系统兼容 Id 试。

![设备报告它具有其函数的任何兼容 id。](images/mbim6.png)

设备报告它具有其函数的任何兼容 ID。 USBCCGP 然后子设备节点的每个函数中创建设备。

## <a name="mbim-backward-compatible-functions"></a>MBIM 向后兼容功能


MBIM NCM 1.0 规范与向后兼容的功能就会出现作为 NCM 1.0 函数默认情况下。 包含 MBIM 向后兼容函数的移动宽带设备报告的 Microsoft 操作系统兼容 ID 为"MBIM"以便 MBIM 函数。 这样，Windows 8 来检测为 MBIM 函数 NCM 1.0 函数和加载 MBCD 作为函数驱动程序。

 

 





