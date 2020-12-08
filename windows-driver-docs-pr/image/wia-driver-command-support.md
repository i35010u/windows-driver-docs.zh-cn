---
title: WIA 驱动程序命令支持
description: WIA 驱动程序命令支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b3ee23c23b245622aaad9861354cbfa9a6003ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818934"
---
# <a name="wia-driver-command-support"></a>WIA 驱动程序命令支持





WIA 设备命令是由 WIA 服务 (代表) 到 WIA 微型驱动程序的图像应用程序发送的请求，指示它执行特定操作。

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
<td><p>转到下一个文档 (仅) 发送到了个专用扫描仪。</p></td>
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
<td><p>仅)  (向照相机发送图片。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_UNLOAD_DOCUMENT</p></td>
<td><p>卸载仅)  (颁发给专用扫描仪的当前文档。</p></td>
</tr>
</tbody>
</table>

 

\_ \_ Microsoft Windows SDK 文档中介绍了 WIA CMD XXX 命令。 您可以包括您自己的自定义命令列表。

### <a name="adding-device-command-support"></a>添加设备命令支持

若要将 WIA 微型驱动程序正确设置为报表设备命令，请在 [**IWiaMiniDrv：:D rvgetcapabilities**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities) 方法中报告支持的命令的数组。 有关 **IWiaMiniDrv：:D rvgetcapabilities** 方法的实现示例，请参阅 [添加中断事件支持](adding-interrupt-event-support.md)。

### <a name="implementing-the-iwiaminidrvdrvdevicecommand-method"></a>实现 IWiaMiniDrv：:d rvDeviceCommand 方法

WIA 服务调用 [**IWiaMiniDrv：:D rvdevicecommand**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand) 方法来响应应用程序对 **IWiaItem：:D evicecommand** 方法的调用， (Microsoft Windows SDK 文档) 中所述。 **IWiaMiniDrv：:D rvdevicecommand** 方法应执行以下任务：

1.  确定发送的命令是否是受支持的命令。

2.  处理命令请求。

WIA 驱动程序应使用 *pWiasContext* 指针确定要接收设备命令的 WIA 项。 WIA 驱动程序应随后处理收到的设备命令，该命令以传入的 WIA 项为目标。 发送到不受支持的 WIA 驱动程序的任何命令都应该失败，并出现电子 \_ INVALIDARG 错误代码。

有关 **IWiaMiniDrv：:D rvdevicecommand** 方法的实现示例，请参阅向 [应用程序通知项树更改](informing-an-application-of-item-tree-changes.md)。
