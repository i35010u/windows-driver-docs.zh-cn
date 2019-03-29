---
title: WIA 驱动程序命令支持
description: WIA 驱动程序命令支持
ms.assetid: 9c552316-7dd6-4102-88d3-fab9732d1e5d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b9346832723f38f7bbf10784807153abe7cc0cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566268"
---
# <a name="wia-driver-command-support"></a>WIA 驱动程序命令支持





WIA 设备命令是 WIA 微型驱动程序，指示它执行特定操作发送由 WIA 服务 （代表图像处理应用程序） 的请求。

以下是可以颁发给微型驱动程序的 WIA 设备命令的列表：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Command</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_CMD_CHANGE_DOCUMENT</p></td>
<td><p>将更改为下一个文档 （颁发给仅多文档扫描仪）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_DELETE_ALL_ITEMS</p></td>
<td><p>删除驱动程序项树。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CMD_DIAGNOSTIC</p></td>
<td><p>保留 Microsoft。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_SYNCHRONIZE</p></td>
<td><p>重新生成驱动程序项树。 所有微型驱动程序必须支持此命令。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CMD_TAKE_PICTURE</p></td>
<td><p>拍摄照片 （颁发给仅相机）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_UNLOAD_DOCUMENT</p></td>
<td><p>卸载当前文档 （颁发给仅多文档扫描仪）。</p></td>
</tr>
</tbody>
</table>

 

WIA\_CMD\_XXX 命令 Microsoft Windows SDK 文档中所述。 您可以包括您自己自定义命令的列表。

### <a name="adding-device-command-support"></a>添加设备的命令支持

若要正确设置为报告设备的命令将 WIA 微型驱动程序，报告中受支持的命令数组[ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)方法。 有关示例实现**IWiaMiniDrv::drvGetCapabilities**方法，请参阅[添加中断事件支持](adding-interrupt-event-support.md)。

### <a name="implementing-the-iwiaminidrvdrvdevicecommand-method"></a>实现 IWiaMiniDrv::drvDeviceCommand 方法

WIA 服务调用[ **IWiaMiniDrv::drvDeviceCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff543967)方法以响应应用程序的调用**IWiaItem::DeviceCommand**方法 (中所述Microsoft Windows SDK 文档)。 **IWiaMiniDrv::drvDeviceCommand**方法应执行以下任务：

1.  确定是否发送的命令支持的命令。

2.  处理该命令请求。

WIA 驱动程序应确定是使用接收设备命令的 WIA 项*pWiasContext*指针。 WIA 驱动程序应然后处理接收到的设备命令针对传入 WIA 项。 发送到 WIA 驱动程序不受支持的任何命令应失败，电子\_INVALIDARG 错误代码。

有关示例实现**IWiaMiniDrv::drvDeviceCommand**方法，请参阅[通知项树更改应用程序](informing-an-application-of-item-tree-changes.md)。
