---
title: 静态图像设备的 INF 文件
description: 静态图像设备的 INF 文件
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 367535b99cf048a818a589fd92450a53309f9500
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793683"
---
# <a name="inf-files-for-still-image-devices"></a>静态图像设备的 INF 文件

静态映像设备的默认类安装程序 *sti \_ci.dll* 可识别一组特殊的 INF 文件条目。 在 INF 文件中，这些条目必须位于设备的 [**INF DDInstall 部分**](../install/inf-ddinstall-section.md)中。 下表中描述了这些条目。

| INF 文件条目 | 值 | 注释 |
| --- | --- | --- |
| 类别 | StillImage | 必须 |
| DeviceType | 1用于扫描仪，2适用于照相机，3用于视频设备 | 必须 |
| DeviceSubType | 供应商定义的值 | 可选 |
| 连接 | 对于连接到串行端口或并行端口的非 PnP 设备，这可能是串行或并行的，以限制用户在安装过程中选择的端口。 | 可选。<br>如果未指定，则用户可以选择任何串行端口或并行端口。 |
| 功能 | 指定一个数字，该数字将转换为标识设备功能的位标志。 这些标志存储在注册表中，并且通过 [STI_DEV_CAPS](/windows-hardware/drivers/ddi/sti/ns-sti-_sti_dev_caps) 结构可供 Microsoft STI 组件使用。<br><br>位0−设置/清除 STI_DEV_CAPS 中的 STI_GENCAP_NOTIFICATIONS<br>第1位−设置/清除 STI_DEV_CAPS 中的 STI_GENCAP_POLLING_NEEDED<br>第2位−设置/清除 STI_DEV_CAPS 中的 STI_GENCAP_GENERATE_ARRIVALEVENT<br>第3位−设置/清除 STI_DEV_CAPS 中的 STI_GENCAP_AUTO_PORTSELECT | 可选 |
| PropertyPages | 标识为 [静态图像设备](property-sheet-pages-for-still-image-devices.md)创建自定义属性页的 DLL 的名称和入口点。<br>下面的示例标识 DLL、 *estp2cpl.dll*，以及此 dll 中的 **EnumStiPropPages** 入口点。 入口点名称是可选的;如果省略，则入口点默认为 **EnumStiPropPages**。<br><br>`PropertyPages = estp2cpl.dll, EnumStiPropPages`<br><br> | 可选 |
| DeviceData | 标识供应商提供的数据部分，其中包含要存储在注册表中的信息，在 **DeviceData** 项下。 对于 TWAIN 支持的设备，data 部分必须包含 **TwainDS** 条目。 有关详细信息，请参阅 [供应商可修改的注册表值](registry-entries-for-still-image-devices.md#ddk-vendor-modifiable-registry-values-si) | 可选。<br>但是，此项是 [创建 Push-Model 感知应用程序](creating-push-model-aware-applications.md)所必需的。 |
| 事件 | 标识供应商提供的数据部分，其中列出了仍为图像设备事件。 本节中的每个条目都必须采用以下格式：<br><br>`EventName="String",{GUID},App`<br><br>*事件名称是事件* 的内部名称， *String* 是事件的显示字符串， *guid* 是事件的 Guid，请参阅 [静止图像设备事件](still-image-device-events.md)， *应用* 程序指定发生事件时要启动的图像处理应用程序。 若要启动当前已注册的应用程序，请使用 ( * ) *应用* 程序的星号。 | 可选。<br>但是，此项是 [创建 Push-Model 感知应用程序](creating-push-model-aware-applications.md)所必需的。 |
| UninstallSection | 指向 INF 部分，通常包含 [Inf DelFiles 指令](../install/inf-delfiles-directive.md) 和 [inf DelReg 指令](../install/inf-delreg-directive.md)。 此部分中的条目采用以下格式：<br><br>`UninstallSection=UninstallSectionName`<br><br>*UninstallSectionName* 是包含 **Delfiles** 或 **DelReg** 指令的节的名称。 请注意， **Windows 文件保护** 可能会禁止用户删除某些文件，即使使用 **DelFiles** 指令指定了这些文件也是如此。 | 可选。<br>此项仅对 Windows 2000 有效。 |

静止映像设备的默认类安装程序支持标准 [INF CopyFiles 指令](../install/inf-copyfiles-directive.md)。 安装程序对组件文件使用内部引用计数器，因此在卸载操作过程中不会提前删除由多个设备共享的文件。

静态映像设备（ *sti*）的默认 INF 文件为每种设备类型定义了两个安装节，如下所示：

- [INF DDInstall 部分](../install/inf-ddinstall-section.md)，必须在供应商提供的 INF 文件的 *DDInstall* 部分中引用，如下表所示。

| USB 设备 | SCSI 设备 | 串行设备 |
| --- | --- | --- |
| `Include=sti.inf`<br><br>`Needs=STI.USBSection` | `Include=sti.inf`<br><br>`Needs=STI.SCSISection`  | `Include=sti.inf`<br><br>`Needs=STI.SerialSection` |

- [INF DDInstall 部分](../install/inf-ddinstall-services-section.md)，必须在 *DDInstall* 中引用。供应商提供的 INF 文件的 "**服务**" 部分，如下表所示。

| USB 设备 | SCSI 设备 | 串行设备 |
| --- | --- | --- |
| `Include=sti.inf`<br><br>`Needs=STI.USBSection.Services` | `Include=sti.inf`<br><br>`Needs=STI.SCSISection.Services`  | `Include=sti.inf`<br><br>`Needs=STI.SerialSection.Services` |

如果还 [为映像采集 api 创建设备特定的组件](creating-device-specific-components-for-image-acquisition-apis.md)，则通常会在 INF 文件中包含这些组件的文件名。

有关为静止图像设备创建 INF 文件的其他指南，你可以查看随 Windows 提供的包含 "子类 = StillImage" 条目的任何 INF 文件。

## <a name="remarks"></a>备注

在为扫描仪开发 INF 文件时，可以使用 [MICROSOFT OS 描述符](/previous-versions/gg463179(v=msdn.10)) 来启用兼容 ID 功能。 当你执行此操作时，你允许一个扫描仪驱动程序与多个扫描仪模型兼容。
