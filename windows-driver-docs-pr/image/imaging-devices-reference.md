---
title: 图像处理设备引用
description: 图像处理设备引用
ms.assetid: 2ee6ce92-44dc-4c59-a438-f65b41f3b43a
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf2827957c41ad45ee3253752e41ee5a235edac2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373531"
---
# <a name="imaging-devices-reference"></a>图像处理设备引用

本部分包含有关以下技术参考信息：

[图像处理设备的设备接口类](device-interface-classes-for-imaging-devices.md)

[IWiaMiniDrv 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)

[静止图像接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)

[基于设备的 Web 服务参考](https://docs.microsoft.com/windows-hardware/drivers/image/web-services-on-devices-reference)

## <a name="wia-and-sti-driver-reference-table"></a>WIA 和 STI 驱动程序参考表

下表包含用于 Windows 图像采集 (WIA) 驱动程序和仍映像 (STI) 驱动程序的参考信息。 这些驱动程序控制的设备，包括扫描仪和照相机，捕获静止图像。 有关这些驱动程序的详细信息，请参阅[Windows 图像采集驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)并[仍映像驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)。

以下部分介绍接口、 函数、 结构和所用的 WIA 和 STI 驱动程序属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>部分</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="device-interface-classes-for-imaging-devices.md" data-raw-source="[Device Interface Classes for Imaging Devices](device-interface-classes-for-imaging-devices.md)">图像处理设备的设备接口类</a></p></td>
<td><p>图像处理设备的设备类 GUID。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv" data-raw-source="[IWiaMiniDrv Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)">IWiaMiniDrv 接口</a></p></td>
<td><p>用于管理 WIA 微型驱动程序和 WIA 服务之间的所有通信的接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/index" data-raw-source="[WIA Driver Services Library Functions](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/index)">WIA 驱动程序服务库函数</a></p></td>
<td><p>用于管理设备的项和数据传输的 WIA 微型驱动程序的帮助程序函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="wia-properties.md" data-raw-source="[WIA Properties](wia-properties.md)">WIA 属性</a></p></td>
<td><p>WIA 的设备，包括状态、 功能和设备标识信息的属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[WIA Utility Library Functions and Classes](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">WIA 实用工具库函数和类</a></p></td>
<td><p>实用工具函数和由 WIA 微型驱动程序，以支持调试，并执行常见任务的类。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback" data-raw-source="[IWiaMiniDrvCallBack Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)">IWiaMiniDrvCallBack Interface</a></p></td>
<td><p>WIA 服务和 WIA 微型驱动程序之间传输状态和图像数据的回调接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem" data-raw-source="[IWiaDrvItem Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)">IWiaDrvItem 接口</a></p></td>
<td><p>WIA 微型驱动程序用于管理 WIA 驱动程序项树的接口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiaerrorhandler" data-raw-source="[IWiaErrorHandler Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiaerrorhandler)">IWiaErrorHandler 接口</a></p></td>
<td><p>接口由 WIA 微型驱动程序，用于提供错误状态，以支持错误恢复。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiaimagefilter" data-raw-source="[IWiaImageFilter Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiaimagefilter)">IWiaImageFilter 接口</a></p></td>
<td><p>接口实现的图像处理筛选器，并由与筛选器进行通信的 WIA 服务调用。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[IWiaLog Interface and Diagnostic Log Macros](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">IWiaLog 界面和诊断日志宏</a></p></td>
<td><p>接口和记录跟踪、 错误和警告消息到诊断日志文件到 WIA 微型驱动程序使用的宏。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiasegmentationfilter" data-raw-source="[IWiaSegmentationFilter Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiasegmentationfilter)">IWiaSegmentationFilter Interface</a></p></td>
<td><p>WIA 微型驱动程序用于分段图像中检测区域的接口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiatransfercallback" data-raw-source="[IWiaTransferCallback Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiatransfercallback)">IWiaTransferCallback Interface</a></p></td>
<td><p>接口实现的图像处理筛选器，由要启动的图像流处理的 WIA 服务调用。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[WIA Microdriver Functions, Structures, and Commands](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">WIA Microdriver 函数、 结构和命令</a></p></td>
<td><p>函数、 结构和使用 WIA microdrivers 的命令。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiadevd/index" data-raw-source="[WIA User Interface Extensions](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiadevd/index)">WIA 用户界面扩展</a></p></td>
<td><p>使用设备供应商提供了其设备的自定义用户接口的接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[WIA Structures](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">WIA 结构</a></p></td>
<td><p>使用的驱动程序级别 WIA 方法和函数的结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[Still Image Interfaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">静止图像接口</a></p></td>
<td><p>接口、 结构、 数据类型和 STI 驱动程序使用的控制代码。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema" data-raw-source="[Web Services on Devices Reference](https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema)">基于设备的 Web 服务参考</a></p></td>
<td><p>基于设备的信息，包括扫描服务 （WS-扫描） 的 web 服务</p></td>
</tr>
</tbody>
</table>

 

 

 





