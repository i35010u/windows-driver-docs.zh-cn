---
title: 扩展单元插件体系结构
description: 扩展单元插件体系结构
ms.assetid: cf2b32dd-0b65-41ce-b6e8-a9068e232600
keywords:
- 扩展单位 WDK USB 视频类，体系结构
- 扩展单元控制 WDK USB 视频类
- 注册表 WDK USB 视频类
- 事件 WDK USB 视频类
- COM API WDK USB 视频类
- 插件 DLL WDK USB 视频类
- 扩展单元
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c7985c2bf5c698dc6715242b219d7e8ba8ffc4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384100"
---
# <a name="extension-unit-plug-in-architecture"></a>扩展单元插件体系结构


USB 视频类驱动程序公开为 USB 视频 KS 代理筛选器中的节点扩展单元。 扩展单元控件的属性的类型 KSNODETYPE 在节点上设置作为进一步公开在用户模式下\_开发人员\_特定。 属性集的 GUID 匹配的扩展单元描述符的 GUID。

单个扩展单元控件应为连续编号从 1 到某个最大值*n*。 这些控件将直接映射到属性标识符 (Id) 上的扩展单元属性集，并且可以使用标准 KSPROPERTY 请求通过访问[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-ikscontrol)。

在应用程序属性的请求响应，UVC 驱动程序将返回具有的属性值**MembersFlags**的成员[ **KSPROPERTY\_MEMBERSHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_membersheader)结构设置以独占方式为 KSPROPERTY\_成员\_范围。 UVC 执行不支持单步执行范围或任意长度的扩展单位默认值。

若要公开的应用程序的扩展单元属性，您可以编写用户模式下插件 DLL 并公开 COM API。 您可以通过使用设置的 KS 属性向发出请求来实现此 API **IKsControl**接口。 *Vidcap.ax*节点接口插件基于某些注册表条目将自动加载。 应用程序可以通过使用访问接口**IKsTopologyInfo::CreateNodeInstance**调用后跟**QueryInterface**上获取所需的 COM API 的节点对象。

以下元素需要编写和使用插件扩展单元：

- 实现扩展单元 API 和接口的标头和 cpp 文件命名为 IKsNodeControl。 Vidcap.ax 使用 IKsNodeControl 接口通知插件的扩展节点标识符并将其提供与 IKsControl 的实例。 有关这些文件可在示例代码[示例扩展单元插件 DLL](sample-extension-unit-plug-in-dll.md)。

- *.Rgs*注册的节点接口和类 Id (Clsid) 下的文件**HKLM\\系统\\CCS\\控制\\NodeInterfaces\\** <em>属性\_设置\_GUID</em>注册表子项。 此注册表子项中的条目包含的接口 ID (IID) 和 CLSID 的二进制值。 有关详细信息，请参阅[UVC 扩展单位的示例注册表项](sample-registry-entry-for-uvc-extension-units.md)。

- 应用程序调用此接口。 应用程序首次创建节点实例使用正确的节点 ID 使用 IKsTopologyInfo::CreateNodeInstance。 然后，应用程序调用**QueryInterface**节点实例以获取所需的扩展单元接口上。 有关详细信息，请参阅[UVC 扩展单位的示例应用程序](sample-application-for-uvc-extension-units.md)和[扩展单位支持自动更新事件](supporting-autoupdate-events-with-extension-units.md)

在本部分中的代码示例演示所有这些元素。 请参阅[生成扩展单元示例控件](building-the-extension-unit-sample-control.md)若要了解如何生成示例插件和关联的示例应用程序代码。

注册插件 DLL 并提供了上面所述的注册表项后，Vidcap.ax 创建节点实例时将自动加载相关节点接口。

**请注意**  自 Windows XP SP2 起支持的扩展单元属性集，仅在节点上，而不是在筛选器。

 

### <a name="registry-considerations"></a>注册表注意事项

若要注册的 IID 和 CLSID 的插件导出的接口，可以使用 DLL 注册或特定于设备的安装程序信息 (INF) 文件。

请参阅[UVC 扩展单位的示例注册表项](sample-registry-entry-for-uvc-extension-units.md)有关的示例 *.rgs*文件，演示所需的注册表项值。 本主题还演示如何编写特定于设备的 INF 文件来安装 USB 视频设备并注册插件 DLL。 您可以选择 DLL 注册或特定于设备的 INF 文件中，根据特定需求。

### <a name="schematic"></a>示意图

将以下示意图显示了在编写和使用插件扩展单元中所涉及的各种模块之间的关系。 具体而言，它跟踪应用程序中，对插件 DLL，向驱动程序连接，最后到在设备本身的扩展单元。 示意图还说明了各种 Guid 涉及;通过使用匹配的颜色突出显示相同的值。

![说明扩展单元插件和关联模块的关系图](images/usbvidextension.gif)

### <a name="eventing-mechanisms"></a>事件处理机制

USB 视频类支持自动更新事件，其中设备通知中的任何其控件的更改主机驱动程序。 Microsoft USB 视频类驱动程序通过让注册自动更新事件的应用程序支持这一概念。 获取更新的过程涉及三个步骤：

1.  使用注册更新事件[KSEVENTSETID\_VIDCAPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vidcapnotify)::[**KSEVENT\_VIDCAP\_自动\_更新**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcap-auto-update)

2.  侦听通知的事件句柄上的事件

3.  正在取消通知完成时

 

 




