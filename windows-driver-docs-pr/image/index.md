---
title: 图像处理设备驱动程序设计指南
description: 图像处理设备驱动程序设计指南
ms.assetid: dfdeeec8-bd06-452a-9189-87b20ce27699
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 7c364274cad46783a367a2befa98df20d299531d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189161"
---
# <a name="imaging-device-driver-design-guide"></a>图像处理设备驱动程序设计指南


本部分包含有关 Windows 图像采集 (WIA) 驱动程序、静止图像 (STI) 驱动程序和基于设备的 Web 服务 (WSD) 的信息。

> [!NOTE]
> WIA 编程接口用于为现代 Windows 操作系统开发图像处理驱动程序。 STI 编程接口用于为旧的 Windows 操作系统开发图像处理驱动程序。 STI 编程接口文档将存档在将来的版本中。 

## <a name="in-this-section"></a>本部分内容

- [图像处理设备的设备接口类](device-interface-classes-for-imaging-devices.md)

- [Windows 图像采集驱动程序](windows-image-acquisition-drivers.md)

- [WIA 属性](about-wia-properties.md)

- [64 位和 WIA](64-bit-and-wia.md)

- [WIA 兼容性层](wia-compatibility-layer.md)

- [WIA 驱动程序筛选器](wia-driver-filters.md)

- [WIA 项树](wia-item-trees.md)

- [包含设备 Web 服务的 WIA](wia-with-web-services-for-devices.md)

- [开发 WIA 驱动程序](developing-a-wia-driver.md)

- [开发 WIA 相机驱动程序](developing-a-wia-camera-driver.md)

- [WIA 微型驱动程序最佳做法](wia-minidriver-best-practices.md)

- [WIA 微驱动程序命令](wia-microdriver-commands.md)

- [生成、排查和调试 WIA 微型驱动程序](building--troubleshooting-and-debugging-wia-minidrivers.md)

- [WIA 示例和工具](wia-samples-and-tools.md)

- [静止图像驱动程序](still-image-drivers.md)

- [基于设备的 Web 服务](web-services-on-devices.md)

- [基于设备的 Web 服务参考](web-services-on-devices-reference.md)

## <a name="wia-and-sti-driver-reference"></a>WIA 和 STI 驱动程序参考

下表包含 Windows 图像获取 (WIA) 驱动程序和静止成像 (STI) 驱动程序的参考信息。 这些驱动程序控制用于捕获静止图像的设备，包括扫描仪和照相机。 有关这些驱动程序的详细信息，请参阅 [Windows 图像采集驱动程序](./windows-image-acquisition-drivers.md)和[静态图像驱动程序](./still-image-drivers.md)。

以下各节介绍 WIA 和 STI 驱动程序所使用的接口、函数、结构和属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>部分</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="device-interface-classes-for-imaging-devices.md" data-raw-source="[Device Interface Classes for Imaging Devices](device-interface-classes-for-imaging-devices.md)">图像处理设备的设备接口类</a></p></td>
<td><p>成像设备的设备类 GUID。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv" data-raw-source="[IWiaMiniDrv Interface](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)">IWiaMiniDrv 接口</a></p></td>
<td><p>用于管理 WIA 微型驱动程序和 WIA 服务之间的所有通信的接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/index" data-raw-source="[WIA Driver Services Library Functions](/windows-hardware/drivers/ddi/wiamdef/index)">WIA 驱动程序服务库函数</a></p></td>
<td><p>WIA 微型驱动程序用于管理设备项和数据传输的 Helper 函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="wia-properties.md" data-raw-source="[WIA Properties](wia-properties.md)">WIA 属性</a></p></td>
<td><p>WIA 设备的属性，包括状态、功能和设备标识信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Utility Library Functions and Classes](/windows-hardware/drivers/ddi/_image/index)">WIA 实用工具库函数和类</a></p></td>
<td><p>WIA 微型驱动程序用于支持调试和执行常见任务的实用工具函数和类。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback" data-raw-source="[IWiaMiniDrvCallBack Interface](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)">IWiaMiniDrvCallBack 接口</a></p></td>
<td><p>用于在 WIA 服务和 WIA 微型驱动程序之间传输状态和图像数据的回调接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem" data-raw-source="[IWiaDrvItem Interface](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)">IWiaDrvItem 接口</a></p></td>
<td><p>WIA 微型驱动程序用于管理 WIA 驱动程序项树的接口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaerrorhandler" data-raw-source="[IWiaErrorHandler Interface](/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaerrorhandler)">IWiaErrorHandler 接口</a></p></td>
<td><p>WIA 微型驱动程序用来提供错误状态和支持错误恢复的接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaimagefilter" data-raw-source="[IWiaImageFilter Interface](/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaimagefilter)">IWiaImageFilter 接口</a></p></td>
<td><p>由图像处理筛选器实现并由 WIA 服务调用以用来与筛选器通信的接口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[IWiaLog Interface and Diagnostic Log Macros](/windows-hardware/drivers/ddi/_image/index)">IWiaLog 接口和诊断日志宏</a></p></td>
<td><p>WIA 微型驱动程序用于将跟踪、错误和警告消息记录到诊断日志文件的接口和宏。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiasegmentationfilter" data-raw-source="[IWiaSegmentationFilter Interface](/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiasegmentationfilter)">IWiaSegmentationFilter 接口</a></p></td>
<td><p>WIA 微型驱动程序用来检测分段图像中的区域的接口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiatransfercallback" data-raw-source="[IWiaTransferCallback Interface](/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiatransfercallback)">IWiaTransferCallback 接口</a></p></td>
<td><p>由图像处理筛选器实现并由 WIA 服务调用以用来启动图像流处理的接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Microdriver Functions, Structures, and Commands](/windows-hardware/drivers/ddi/_image/index)">WIA 微驱动程序函数、结构和命令</a></p></td>
<td><p>WIA 微驱动程序使用的函数、结构和命令。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiadevd/index" data-raw-source="[WIA User Interface Extensions](/windows-hardware/drivers/ddi/wiadevd/index)">WIA 用户界面扩展</a></p></td>
<td><p>设备供应商用于为其设备提供自定义用户界面的接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Structures](/windows-hardware/drivers/ddi/_image/index)">WIA 结构</a></p></td>
<td><p>驱动程序级 WIA 方法和函数使用的结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[Still Image Interfaces](/windows-hardware/drivers/ddi/_image/index)">静止图像接口</a></p></td>
<td><p>STI 驱动程序所使用的接口、结构、数据类型和控制代码。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema" data-raw-source="[Web Services on Devices Reference](./scan-service--ws-scan--schema.md)">基于设备的 Web 服务参考</a></p></td>
<td><p>设备上的 Web 服务信息，包括扫描服务 (WS-SCAN)</p></td>
</tr>
</tbody>
</table>

## <a name="related-sections"></a>相关章节

- [图像处理 DDI 参考](/windows-hardware/drivers/ddi/_image)