---
title: MB 联合函数描述符
description: 本部分介绍适用于 MB 设备的联合函数描述符和 MBIM 后向兼容函数
ms.assetid: 4B8C63DD-4B8D-40AB-A6DF-0466343E7E45
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc4b35107147fb56cdb82e80f0a519eff4c4c777
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844272"
---
# <a name="mb-union-function-descriptors"></a>MB 联合功能描述符


## <a name="union-function-descriptors"></a>联合函数描述符


对于 CDC 设备，实现 Ufd 的移动宽带设备的设备类/子类/协议为 2/0/0。 这会阻止 Windows 在设备上加载 USBCCGP。 有关 Windows 如何在复合设备上加载 USBCCGP 的信息，请参阅[USB 通用父驱动程序（USBCCGP）](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

若要允许 Windows 加载 USBCCGP，当设备未配置时，设备需要报告 Microsoft OS 兼容 ID "CDC\_WMC"。 检测到 "CDC\_WMC" 的兼容 ID 后，Windows 将加载 USBCCGP，并将设备上的配置设置为1。 然后，USBCCGP 将再次查询 Microsoft OS 兼容 Id。 但是，这一次，设备不应报告 "CDC\_WMC" 的 Microsoft OS 兼容 ID。 设备可能会报告所选配置中的函数的 Microsoft OS 兼容 Id。

![未配置设备时，对 microsoft os 描述符的 usbhub 查询](images/mbim1.png)

未配置设备时，对 Microsoft OS 描述符的 USBHUB 查询

![设备通过 cdc\-wmc 进行响应，这将导致 windows 加载 usbccgp。](images/mbim2.png)

设备以 "CDC\_WMC" 进行响应，这将导致 Windows 加载 USBCCGP

![usbccgp 选择设备上的配置 \#1。](images/mbim3.png)

USBCCGP 选择设备上的配置 \#1。

![设备选择配置并推移兼容 id 列表。](images/mbim4.png)

设备选择配置并推移兼容 Id 列表。 该设备可能包括 CompatID2，这对于 Function2 是必需的。

![加载后，usbccgp 再次查询 microsoft os 兼容 id。](images/mbim5.png)

加载后，USBCCGP 再次查询 Microsoft OS 兼容 Id。

![设备报告其功能的所有兼容 id。](images/mbim6.png)

设备报告其功能的所有兼容 ID。 然后，USBCCGP 为设备中的每个函数创建子设备节点。

## <a name="mbim-backward-compatible-functions"></a>MBIM 向后兼容的函数


默认情况下，MBIM 函数与 NCM 1.0 1.0 规范向后兼容。 由 MBIM 向后兼容的函数组成的移动宽带设备应报告 MBIM 函数的 Microsoft OS 兼容 ID "MBIM"。 这允许 Windows 8 检测 NCM 1.0 函数作为 MBIM 函数，并将 MBCD 作为函数驱动程序进行加载。

 

 





