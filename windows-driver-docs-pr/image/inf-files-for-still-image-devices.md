---
title: 静态图像设备的 INF 文件
description: 静态图像设备的 INF 文件
ms.assetid: f68ba904-9049-4f7e-9903-fdf6f413a1a5
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: bc4aec4498ba796cd832a592772f7a05a7b863fa
ms.sourcegitcommit: c4dc4a78ea33537bd47fc7fb666cfd0718d302e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58349262"
---
# <a name="inf-files-for-still-image-devices"></a>静态图像设备的 INF 文件

静止图像设备的默认类安装程序*sti\_ci.dll*，可以识别一组特殊的 INF 文件条目。 在 INF 文件中，这些项必须放置在设备的[ **INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)。 下表所述的条目。

| INF 文件条目 | 值 | 备注 |
| --- | --- | --- |
| SubClass | StillImage | 必需 |
| DeviceType | 1 表示扫描仪，2 表示照相机，适用于视频设备 3 | 必需 |
| DeviceSubType | 供应商定义的值 | 可选 |
| 连接 | 对于非 PnP 设备连接到串行或并行端口，这可能是串行或并行在安装过程中限制用户选择的端口。 | 可选。<br>如果未指定，则用户可以选择任何串行或并行端口。 |
| 功能 | 指定一个数字，将转换为位标志识别设备功能。 这些标志在注册表中存储和适用于通过 Microsoft STI 组件[STI_DEV_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/ns-sti-_sti_dev_caps)结构。<br><br>在 STI_DEV_CAPS 位 0 − 集/清除 STI_GENCAP_NOTIFICATIONS<br>在 STI_DEV_CAPS 位 1 − 集/清除 STI_GENCAP_POLLING_NEEDED<br>在 STI_DEV_CAPS 位 2 − 集/清除 STI_GENCAP_GENERATE_ARRIVALEVENT<br>在 STI_DEV_CAPS 位 3 − 集/清除 STI_GENCAP_AUTO_PORTSELECT | 可选 |
| PropertyPages | 标识一个 DLL，它会创建自定义的名称和入口点[静止图像设备的属性表页](property-sheet-pages-for-still-image-devices.md)。<br>下面的示例标识 DLL *estp2cpl.dll*，并将**EnumStiPropPages**此 DLL 中的入口点。 入口点名称是可选的;如果省略，入口点默认为**EnumStiPropPages**。<br><br>`PropertyPages = estp2cpl.dll, EnumStiPropPages`<br><br> | 可选 |
| DeviceData | 标识包含信息存储在注册表中下的供应商提供的数据部分**DeviceData**密钥。 对于 TWAIN 支持的设备，必须包含的数据部分**TwainDS**条目。 有关详细信息，请参阅[供应商可修改的注册表值](registry-entries-for-still-image-devices.md#ddk-vendor-modifiable-registry-values-si) | 可选。<br>但是，此项是必需的有关[创建推送模型意识的应用程序](creating-push-model-aware-applications.md)。 |
| 事件 | 标识某个供应商提供的数据部分列出了静止图像设备事件。 在本部分中的每个条目必须具有以下格式：<br><br>`EventName="String",{GUID},App`<br><br>*EventName*是事件的内部名称，*字符串*是事件的显示字符串*GUID*是事件的 GUID，请参阅[仍映像设备事件](still-image-device-events.md)，和*应用*指定在事件发生时启动的映像应用程序。 若要启动当前已注册的应用程序，请使用星号 （*） 用于*应用*。 | 可选。<br>但是，此项是必需的有关[创建推送模型意识的应用程序](creating-push-model-aware-applications.md)。 |
| UninstallSection | 指向通常包含一个 INF 部分[INF DelFiles 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)并[INF DelReg 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)。 在本部分中的条目采用以下格式：<br><br>`UninstallSection=UninstallSectionName`<br><br>*UninstallSectionName*的节，其中包含名称**Delfiles**或**DelReg**指令。 请注意， **Windows 文件保护**可能会禁止用户删除一些文件，即使它们使用指定**DelFiles**指令。 | 可选。<br>此项是仅对 Windows 2000 有效。 |

静止图像设备的默认类安装程序支持标准[INF CopyFiles 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)。 安装程序使用内部引用计数器组件文件，因此，由多个设备共享的文件不会删除过早卸载操作的过程。

静止图像设备，默认 INF 文件*sti.inf*，定义每个设备类型，两个安装部分，如下所示：

- [INF DDInstall 部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)，其中必须引用内*DDInstall*供应商提供 INF 文件中的以下表所示的部分。

| USB 设备 | SCSI 设备 | 串行设备 |
| --- | --- | --- |
| `Include=sti.inf`<br><br>`Needs=STI.USBSection` | `Include=sti.inf`<br><br>`Needs=STI.SCSISection`  | `Include=sti.inf`<br><br>`Needs=STI.SerialSection` |

- [INF DDInstall.Services 部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)，其中必须引用内*DDInstall*。**服务**供应商提供 INF 文件中的以下表所示的部分。

| USB 设备 | SCSI 设备 | 串行设备 |
| --- | --- | --- |
| `Include=sti.inf`<br><br>`Needs=STI.USBSection.Services` | `Include=sti.inf`<br><br>`Needs=STI.SCSISection.Services`  | `Include=sti.inf`<br><br>`Needs=STI.SerialSection.Services` |

如果你还[创建图像采集 Api 的特定于设备的组件](creating-device-specific-components-for-image-acquisition-apis.md)，通常将 INF 文件中包括这些组件的文件名。

有关创建静止图像设备的 INF 文件中的其他指南，你可以查看任何与包含的项的 Windows 提供的 INF 文件"子类 = StillImage"。

## <a name="remarks"></a>备注

当开发用于扫描程序的 INF 文件后时，可以使用[Microsoft OS 描述符](https://msdn.microsoft.com/library/windows/hardware/gg463179.aspx)启用兼容性 ID 功能。 当执行此操作时，允许一个扫描程序驱动程序与多个扫描程序模型兼容。
