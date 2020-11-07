---
title: 指定多功能设备的硬件 ID
description: 指定多功能设备的硬件 ID
ms.assetid: e45f7564-89a7-49c0-8011-69e5da3d5651
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ead34ffcdbd435dac759cb6048e608c622fe9d2a
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361509"
---
# <a name="specifying-hardware-ids-for-a-multifunction-device"></a>指定多功能设备的硬件 ID


可以为物理设备指定多个 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) 元素。 这是通过在父 [**HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))元素中指定多个 **HardwareID** 元素值来完成的。 每个值必须为设备指定唯一的 [硬件 ID](hardware-ids.md) 。

例如，考虑公司 Contoso，公司的单功能 USB 打印机。以下 **HardwareID** 元素可用于定义设备：

```cpp
<HardwareIDList>
  <HardwareID>DOID:USB\VID_1234&PID_1234&REV_0000</HardwareID>
  <HardwareID>DOID:USB\VID_1234&PID_1234</HardwareID>
  <HardwareID>DOID:USBPRINT\Contoso_Ltd_Co9999/HardwareID>
</HardwareIDList>
```

如果设备是多功能设备，则设备容器会将设备节点中的所有 [硬件 id](hardware-ids.md) 与设备上每个硬件功能 ( *devnodes* ) 组合在一起。 有关设备容器和容器 Id 的详细信息，请参阅 [容器 id](container-ids.md)。

下图显示了多功能设备的 devnodes 和设备容器之间的关系。

![阐释如何将多个 devnodes 中的硬件 id 合并为单个设备容器的关系图](images/hardwareid.png)

根据你的多功能设备，你可以通过在 [**HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))元素中使用单独的 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))元素来确定哪些 [硬件 ID](hardware-ids.md)值是指定的。 在 **HardwareIDList** 元素中，可以按任意顺序指定多个硬件 id。 但是，您应注意以下几点：

-   在给定的 devnode 中，操作系统的硬件 Id 排名是确定性的。 例如，在上图中， *HardwareID1 的* 排名始终高于 *HardwareID1-2* 和 *HardwareID1* 。

-   操作系统不会从一个 devnode 的硬件 ID （比另一个 devnode 中的硬件 ID 高）中一致地排名硬件 ID。 例如，在上图中，操作系统可能并不总是排名高于 *HardwareID2-1* 的 *HardwareID1* 。

因此，请确保元数据包不依赖于设备的 devnodes 中 [硬件 id](hardware-ids.md) 的顺序或排名。 你应在设备元数据包的 [**HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85)) 元素中使用多功能设备的所有相关硬件 id。 这可以保证操作系统选择元数据包，而不考虑硬件 Id 的排名。

根据上图中所示的 *devnode* 拓扑，请考虑以下建议：

-   如果已发布其他仅指定 *HardwareID2-1* 的元数据包，请在新设备元数据包中指定 *HardwareID1-1* 、 *HardwareID2* 和 *硬件 ID3 1* 。

    如果操作系统对 *HardwareID2 的* 排名高于 *HardwareID1-* 1，并且发现在旧的和新的元数据包中同时指定了 *HardwareID2-1* ，则操作系统将根据 [**LastModifiedDate**](/previous-versions/windows/hardware/metadata/ff548624(v=vs.85)) XML 元素的值选择元数据包。 在这种情况下，操作系统会选择新的元数据包。

-   如果新的元数据包仅列出 *HardwareID1-* 1，则当 *HardwareID2 的* 排名高于 *HardwareID1-* 1 时，操作系统将不会选择新的包。

有关元数据包选择和排名的详细信息，请参阅 [DMRC 如何选择设备元数据包](how-the-dmrc-selects-a-device-metadata-package.md)。

 

