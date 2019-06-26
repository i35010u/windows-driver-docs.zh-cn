---
title: 指定多功能设备的硬件 ID
description: 指定多功能设备的硬件 ID
ms.assetid: e45f7564-89a7-49c0-8011-69e5da3d5651
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c381d226c4dea840c7a26f511fbec2a4861548e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385884"
---
# <a name="specifying-hardware-ids-for-a-multifunction-device"></a>指定多功能设备的硬件 ID


您可以指定多个[ **HardwareID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) 。 对于物理设备的元素。 这是通过指定多个**HardwareID**父级范围内的元素值[ **HardwareIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))元素。 每个值必须指定一个唯一[硬件 ID](hardware-ids.md)设备。

例如，考虑来自公司 Contoso，Ltd.的单函数 USB 打印机以下**HardwareID**元素可用于定义设备：

```cpp
<HardwareIDList>
  <HardwareID>DOID:USB\VID_1234&PID_1234&REV_0000</HardwareID>
  <HardwareID>DOID:USB\VID_1234&PID_1234</HardwareID>
  <HardwareID>DOID:USBPRINT\Contoso_Ltd_Co9999/HardwareID>
</HardwareIDList>
```

如果设备是多功能设备，设备容器结合了所有硬件 Id） 为每个设备上的硬件功能。 有关设备的容器和容器 Id 的详细信息，请参阅[容器 Id](container-ids.md)。

下图显示了多功能设备的 devnodes 和设备容器之间的关系。

![关系图说明如何将从多个 devnodes 硬件 id 组合到单个设备容器](images/hardwareid.png)

具体取决于你的多功能设备，你可以决定哪些[硬件 ID](hardware-ids.md)来使用单独指定值[ **HardwareID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))中的元素[**HardwareIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))元素。 可以在任意顺序指定多个硬件 Id **HardwareIDList**元素。 但是，您应注意以下几点：

-   在给定 devnode，由操作系统 Id 的排名是硬件的确定的。 例如，在上图中， *HardwareID1 1*始终排名高于*HardwareID1 2*并*HardwareID1 3*。

-   操作系统不会不一致会以对来自一个 devnode 高于来自另一个 devnode 的硬件 ID 的硬件 ID。 例如，在上图中，操作系统可能不始终会以对*HardwareID1 1*高于*HardwareID2 1*。

因此，请确保您的元数据的包不依赖于顺序或的排名[硬件 Id](hardware-ids.md)跨设备 devnodes。 应为多功能设备中使用所有相关的硬件 Id [ **HardwareIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))你设备元数据包的元素。 这可确保由操作系统选择您的元数据的包而不考虑硬件 Id 的排名。

基于*devnode*上图中所示的拓扑，请考虑以下建议：

-   指定*HardwareID1 1*， *HardwareID2 1*并*硬件 ID3-1*中新的设备元数据包，如果你已发布另一个指定的元数据包仅*HardwareID2 1*。

    如果操作系统等级*HardwareID2 1*高于*HardwareID1 1* ，发现*HardwareID2 1*指定这两种旧的和新的元数据，在包操作系统选择值的基础的元数据程序包[ **LastModifiedDate** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548624(v=vs.85)) XML 元素。 在这种情况下，由操作系统选择新的元数据包。

-   如果新的元数据包只列出*HardwareID1 1*，如果，操作系统将选择新的程序包*HardwareID2 1*排名高于*HardwareID1 1。*

有关元数据的包选择和排名的详细信息，请参阅[如何 dmrc 如何选择设备元数据包](how-the-dmrc-selects-a-device-metadata-package.md)。

 

 





