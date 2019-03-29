---
title: WIA-TWAIN 兼容性
description: WIA-TWAIN 兼容性
ms.assetid: f4fe85cc-a201-4cf7-a0f9-74d7514f1447
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c08b1dea7fd119fdfd6133a7a4bbb233724d7b36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566727"
---
# <a name="wia-twain-compatibility"></a>WIA-TWAIN 兼容性





如果设备可具有两个或多个驱动程序，测试这些驱动程序进行全面的与每个其他的兼容性。 例如，如果一个驱动程序不可用状态 （例如未将关闭会话消息发送某些协议中的驱动程序） 在离开设备，其他驱动程序在尝试与设备通信时可能会失败。 这种情况经常发生与串行设备。

### <a name="wia-and-twain-in-the-same-dll"></a>WIA 和 TWAIN 相同 DLL 中

如果从单个 DLL 同时运行 WIA 驱动程序和 TWAIN 驱动程序，WIA 服务和 TWAIN 应用程序将同时加载此 DLL 的实例。 DLL 的 WIA 实例将生成 WIA 项树。 此树表示的文件夹和摄像机上的映像。 使用 WIA （例如我的电脑或扫描仪和照相机向导） 的任何应用程序将在您的驱动程序中有一份项树。

映像是已删除或添加通过 TWAIN 驱动程序，此更改不通知 WIA 驱动程序。 因此，WIA 项树将包含已删除的映像或将不包含已添加的映像。 在任一情况下，该驱动程序必须刷新其项树。 为此，请 TWAIN 驱动程序必须订购您 WIA 的驱动程序已添加或删除映像时，将刷新其项树。

这是为了调用这样做的一种方法**CoCreateInstance**(CLSID\_**IWiaDevMgr**，...) 从 TWAIN 驱动程序，枚举所有设备，并搜索你的设备。 标识您的驱动程序通过此枚举的一种方法是在您 WIA 的驱动程序中创建自定义属性，以便如果 TWAIN 驱动程序查询此属性，它的存在，您将知道它是您 WIA 的驱动程序。 后**IWiaItem**驱动程序，将命令发送到您的驱动程序以重新生成其树 (例如，将其发送[WIA CMD\_同步](wia-driver-command-support.md)命令，在调用**IWiaItem::DeviceCommand**方法)。 **CoCreateInstance**， **IWiaDevMgr**，和**IWiaItem** Microsoft Windows SDK 文档中所述。

刷新 WIA 项树的另一种方法是创建命名[事件](wia-driver-event-support.md)WIA 驱动程序中。 您 WIA 的驱动程序中的线程可以等待此事件发送信号。 每次删除，或通过 TWAIN 驱动程序添加图像，TWAIN 驱动程序发出信号 (通过调用**SetEvent** （Windows SDK 文档中所述）) 对此命名的事件。 然后将释放 WIA 驱动程序中的线程，并 WIA 驱动程序将重新生成树。

无论哪种方式，您应重新生成树，以便其反映到照相机或扫描仪上的实际映像所做的任何更改。 请确保每当通过添加或删除项在项目树中，更新树排队一个事件 (例如，WIA\_事件\_项\_已删除或 WIA\_事件\_树\_UPDATED （有关这些和其他 WIA 事件标识符的说明，请参阅 Windows SDK 文档）)。 如果您已成功发送到树更改时发生的事件，这将解决我的电脑和不自动更新其他 WIA 应用程序的问题。

**请注意**  时你 TWAIN 和 WIA 驱动程序可能存在于同一个 DLL，WIA，TWAIN 驱动程序不能共享相同的 UI。 每个驱动程序必须具有自己的 UI。

 

 

 




