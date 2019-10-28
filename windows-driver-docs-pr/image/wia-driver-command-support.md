---
title: WIA 驱动程序命令支持
description: WIA 驱动程序命令支持
ms.assetid: 9c552316-7dd6-4102-88d3-fab9732d1e5d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7784bb3fdcfc8eac3e76203a9abdde545a4de086
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840713"
---
# <a name="wia-driver-command-support"></a>WIA 驱动程序命令支持





WIA 设备命令是由 WIA 服务（代表图像应用程序）发送到 WIA 微型驱动程序的请求，指示它执行特定操作。

下面列出了可颁发给微型驱动程序的 WIA 设备命令：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>命令</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_CMD_CHANGE_DOCUMENT</p></td>
<td><p>切换到下一个文档（仅适用于 "专用" 扫描仪）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_DELETE_ALL_ITEMS</p></td>
<td><p>删除驱动程序项树。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CMD_DIAGNOSTIC</p></td>
<td><p>由 Microsoft 保留。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_SYNCHRONIZE</p></td>
<td><p>重新生成驱动程序项树。 所有微型驱动程序都必须支持此命令。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CMD_TAKE_PICTURE</p></td>
<td><p>拍摄照片（仅发到相机）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_UNLOAD_DOCUMENT</p></td>
<td><p>卸载当前文档（仅适用于 "专用" 扫描仪）。</p></td>
</tr>
</tbody>
</table>

 

Microsoft Windows SDK 文档中介绍了 WIA\_CMD\_XXX 命令。 您可以包括您自己的自定义命令列表。

### <a name="adding-device-command-support"></a>添加设备命令支持

若要将 WIA 微型驱动程序正确设置为报表设备命令，请在[**IWiaMiniDrv：:D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)方法中报告支持的命令的数组。 有关**IWiaMiniDrv：:D rvgetcapabilities**方法的实现示例，请参阅[添加中断事件支持](adding-interrupt-event-support.md)。

### <a name="implementing-the-iwiaminidrvdrvdevicecommand-method"></a>实现 IWiaMiniDrv：:d rvDeviceCommand 方法

WIA 服务调用[**IWiaMiniDrv：:D rvdevicecommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)方法，以响应应用程序对**IWiaItem：:D evicecommand**方法的调用（Microsoft Windows SDK 文档中所述）。 **IWiaMiniDrv：:D rvdevicecommand**方法应执行以下任务：

1.  确定发送的命令是否是受支持的命令。

2.  处理命令请求。

WIA 驱动程序应使用*pWiasContext*指针确定要接收设备命令的 WIA 项。 WIA 驱动程序应随后处理收到的设备命令，该命令以传入的 WIA 项为目标。 发送到不受支持的 WIA 驱动程序的任何命令都应该失败，并出现 E\_INVALIDARG 错误代码。

有关**IWiaMiniDrv：:D rvdevicecommand**方法的实现示例，请参阅向[应用程序通知项树更改](informing-an-application-of-item-tree-changes.md)。
