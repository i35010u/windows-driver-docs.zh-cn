---
title: 图像设备参考
description: 图像设备参考
ms.assetid: 2ee6ce92-44dc-4c59-a438-f65b41f3b43a
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1df3a2855b9c19b7b48484ef5ab38c75994c5cbc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840829"
---
# <a name="imaging-devices-reference"></a>图像设备参考

本部分包含以下技术的参考信息：

[图像处理设备的设备接口类](device-interface-classes-for-imaging-devices.md)

[IWiaMiniDrv 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)

[静止图像接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)

[基于设备的 Web 服务参考](https://docs.microsoft.com/windows-hardware/drivers/image/web-services-on-devices-reference)

## <a name="wia-and-sti-driver-reference-table"></a>WIA 和 STI 驱动程序参考表

下表包含 Windows 图像获取（WIA）驱动程序和静止图像（STI）驱动程序的参考信息。 这些驱动程序控制设备（包括扫描仪和照相机）捕获静止图像。 有关这些驱动程序的详细信息，请参阅[Windows 映像获取驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)和[静止映像驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)。

以下各节介绍 WIA 和 STI 驱动程序所使用的接口、函数、结构和属性。

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
<td><p>映像设备的设备类 GUID。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv" data-raw-source="[IWiaMiniDrv Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)">IWiaMiniDrv 接口</a></p></td>
<td><p>用于管理 WIA 微型驱动程序和 WIA 服务之间的所有通信的接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/index" data-raw-source="[WIA Driver Services Library Functions](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/index)">WIA 驱动程序服务库函数</a></p></td>
<td><p>WIA 微型驱动程序用于管理设备项和数据传输的 Helper 函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="wia-properties.md" data-raw-source="[WIA Properties](wia-properties.md)">WIA 属性</a></p></td>
<td><p>WIA 设备的属性，包括状态、功能和设备标识信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Utility Library Functions and Classes](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">WIA 实用工具库函数和类</a></p></td>
<td><p>WIA 微型驱动程序用于支持调试和执行常见任务的实用工具函数和类。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback" data-raw-source="[IWiaMiniDrvCallBack Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)">IWiaMiniDrvCallBack 接口</a></p></td>
<td><p>用于在 WIA 服务和 WIA 微型驱动程序之间传输状态和图像数据的回调接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem" data-raw-source="[IWiaDrvItem Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)">IWiaDrvItem 接口</a></p></td>
<td><p>WIA 微型驱动程序用于管理 WIA 驱动程序项树的接口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaerrorhandler" data-raw-source="[IWiaErrorHandler Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaerrorhandler)">IWiaErrorHandler 接口</a></p></td>
<td><p>WIA 微型驱动程序用来提供错误状态并支持错误恢复的接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaimagefilter" data-raw-source="[IWiaImageFilter Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaimagefilter)">IWiaImageFilter 接口</a></p></td>
<td><p>由由 WIA 服务调用的图像处理筛选器实现的接口，用于与筛选器进行通信。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[IWiaLog Interface and Diagnostic Log Macros](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">IWiaLog 接口和诊断日志宏</a></p></td>
<td><p>WIA 微型驱动程序用于将跟踪、错误和警告消息记录到诊断日志文件的接口和宏。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiasegmentationfilter" data-raw-source="[IWiaSegmentationFilter Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiasegmentationfilter)">IWiaSegmentationFilter 接口</a></p></td>
<td><p>WIA 微型驱动程序用来检测分段图像中的区域的接口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiatransfercallback" data-raw-source="[IWiaTransferCallback Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiatransfercallback)">IWiaTransferCallback 接口</a></p></td>
<td><p>由图像处理筛选器实现并由 WIA 服务调用以启动图像流处理的接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Microdriver Functions, Structures, and Commands](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">WIA Microdriver 函数、结构和命令</a></p></td>
<td><p>WIA microdrivers 使用的函数、结构和命令。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiadevd/index" data-raw-source="[WIA User Interface Extensions](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiadevd/index)">WIA 用户界面扩展</a></p></td>
<td><p>设备供应商用于为其设备提供自定义用户界面的接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Structures](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">WIA 结构</a></p></td>
<td><p>驱动程序级别 WIA 方法和函数使用的结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[Still Image Interfaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">静止图像接口</a></p></td>
<td><p>STI 驱动程序所使用的接口、结构、数据类型和控制代码。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema" data-raw-source="[Web Services on Devices Reference](https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema)">基于设备的 Web 服务参考</a></p></td>
<td><p>设备上的 Web 服务信息，包括扫描服务（WS 扫描）</p></td>
</tr>
</tbody>
</table>

 

 

 





