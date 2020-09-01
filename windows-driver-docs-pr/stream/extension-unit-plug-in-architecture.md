---
title: 扩展单元插件体系结构
description: 扩展单元插件体系结构
ms.assetid: cf2b32dd-0b65-41ce-b6e8-a9068e232600
keywords:
- 扩展单元-WDK USB 视频类，体系结构
- 扩展单元控制 WDK USB 视频类
- 注册表 WDK USB 视频类
- 事件 WDK USB 视频类
- COM API WDK USB 视频类
- 插件 DLL WDK USB 视频类
- 扩展单元
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7818084d60e314600bf2c0659be73f92a8ef30e4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189189"
---
# <a name="extension-unit-plug-in-architecture"></a>扩展单元插件体系结构


USB 视频类驱动程序将扩展单元显示为 USB 视频 KS 代理筛选器中的节点。 扩展单元控件在用户模式下进一步公开为节点上设置的属性，该节点的类型为 KSNODETYPE \_ DEV \_ 特定类型。 属性集的 GUID 与扩展单元描述符的 GUID 匹配。

单个扩展单元控件应连续编号为1到一些最大值 *n*。 这些控件直接映射到扩展单元属性集 (Id) 的属性标识符，并且可以通过 [IKsControl](/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)使用标准 KSPROPERTY 请求访问它们。

为了响应来自应用程序的属性请求，UVC 驱动程序将返回属性值，该属性值将[**KSPROPERTY \_ MEMBERSHEADER**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_membersheader)结构的**MembersFlags**成员专门设置为 KSPROPERTY \_ 成员 \_ 范围。 UVC 不支持按任意长度的分级范围或扩展单元的默认值。

若要向应用程序公开扩展单元属性，可以编写公开 COM API 的用户模式插件 DLL。 可以通过使用 **IKsControl** 接口向 KS 属性集发出请求来实现此 API。 *Vidcap.ax* 根据某些注册表项自动加载节点接口插件。 应用程序可以通过使用 **IKsTopologyInfo：： CreateNodeInstance** ，然后调用节点对象上的 **QueryInterface** 以获取所需的 COM API 来访问接口。

需要以下元素来编写和使用扩展插件单元：

- 实现扩展单元 API 和名为 IKsNodeControl 的接口的标头和 cpp 文件。 Vidcap.ax 使用 IKsNodeControl 接口来通知扩展节点标识符的插件，并为其提供 IKsControl 的实例。 这些文件的示例代码可以在 [示例扩展插件单元 DLL](sample-extension-unit-plug-in-dll.md)中找到。

- 一个 *.rgs*文件，该文件在**HKLM \\ System \\ CCS \\ Control \\ NodeInterfaces \\ **<em>属性 \_ 集 \_ GUID</em>注册表子项下注册节点接口和类 id (clsid) 。 此注册表子项中的条目包含接口 ID (IID) 和 CLSID 的二进制值。 有关详细信息，请参阅 [UVC 扩展单元的示例注册表项](sample-registry-entry-for-uvc-extension-units.md)。

- 调用此接口的应用程序。 应用程序首先使用 IKsTopologyInfo：： CreateNodeInstance 创建具有正确节点 ID 的节点实例。 然后，应用程序对节点实例调用 **QueryInterface** 以获取所需的扩展单元接口。 有关详细信息，请参阅 [UVC 扩展单元的示例应用程序](sample-application-for-uvc-extension-units.md) 和 [支持带扩展单元的自动更新事件](supporting-autoupdate-events-with-extension-units.md)

本节中的代码示例阐释了所有这些元素。 若要了解如何生成示例插件和关联的示例应用程序代码，请参阅 [生成扩展单元示例控件](building-the-extension-unit-sample-control.md) 。

注册插件 DLL 并提供上述注册表项后，Vidcap.ax 会在创建节点实例时自动加载相关节点接口。

**注意**   在 Windows XP SP2 中，只对节点（而不是筛选器）支持扩展单元属性集。

 

### <a name="registry-considerations"></a>注册表注意事项

若要注册插件导出的接口的 IID 和 CLSID，可以使用 DLL 注册或设备特定的设置信息 (INF) 文件。

有关显示注册表项所需值的示例 *.rgs*文件，请参阅[UVC 扩展单元的示例注册表项](sample-registry-entry-for-uvc-extension-units.md)。 本主题还演示如何编写特定于设备的 INF 文件来安装 USB 视频设备和注册插件 DLL。 您可以根据具体需要选择 DLL 注册或特定于设备的 INF 文件。

### <a name="schematic"></a>原理图

以下示意图显示了在编写和使用扩展单元插件时所涉及的各种模块之间的关系。 特别是，它会跟踪应用程序到插件 DLL 的连接，直到驱动程序，最后再到设备本身的扩展单元。 此示意图还说明了所涉及的各种 Guid;相同的值通过使用匹配的颜色突出显示。

![阐释扩展单元插件和关联模块的关系图](images/usbvidextension.gif)

### <a name="eventing-mechanisms"></a>事件机制

USB 视频类支持自动更新事件，其中设备会将其任何控件中的更改通知主机驱动程序。 Microsoft USB 视频类驱动程序通过让应用程序注册自动更新事件来支持此概念。 获取更新的过程涉及三个步骤：

1.  通过使用[KSEVENTSETID \_ VIDCAPNotify](./kseventsetid-vidcapnotify.md)：：[**KSEVENT \_ VIDCAP \_ 自动 \_ 更新**](./ksevent-vidcap-auto-update.md)注册更新事件

2.  侦听通知事件句柄上的事件

3.  完成后取消通知

 

