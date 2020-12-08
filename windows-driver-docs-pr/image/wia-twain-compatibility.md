---
title: WIA-TWAIN 兼容性
description: WIA-TWAIN 兼容性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27998d4d1d355c6ec92a1b737007ccc78052f1eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826387"
---
# <a name="wia-twain-compatibility"></a>WIA-TWAIN 兼容性





如果一个设备可以有两个或多个驱动程序，请彻底测试这些驱动程序以实现彼此兼容。 例如，如果一个驱动程序使设备处于不可用状态 (例如，驱动程序未在某些协议) 中发送关闭会话消息，则当其他驱动程序尝试与设备通信时，该驱动程序可能会失败。 串行设备通常会发生这种情况。

### <a name="wia-and-twain-in-the-same-dll"></a>同一 DLL 中的 WIA 和 TWAIN

如果从单个 DLL 同时运行 WIA 驱动程序和 TWAIN 驱动程序，WIA 服务和 TWAIN 应用程序都将加载此 DLL 的实例。 DLL 的 WIA 实例将生成 WIA 项树。 此树表示相机上的文件夹和图像。 使用 WIA (如我的电脑或扫描仪和照相机向导) 的任何应用程序都将在您的驱动程序中包含项树的副本。

删除或通过 TWAIN 驱动程序添加图像时，不会向 WIA 驱动程序通知此更改。 因此，WIA 项树将包含已删除的映像，或者不包含已添加的映像。 在任一情况下，驱动程序必须刷新其项树。 为此，TWAIN 驱动程序必须对 WIA 驱动程序进行排序，以便在添加或删除图像时刷新其项树。

执行此操作的一种方法是从你的 TWAIN 驱动程序调用 **CoCreateInstance** (CLSID \_ **IWiaDevMgr**,... ) ，枚举所有设备，并搜索你的设备。 通过此枚举标识驱动程序的一种方法是在 WIA 驱动程序中创建自定义属性，以便如果 TWAIN 驱动程序查询此属性并且它存在，您将知道它是 WIA 驱动程序。 获取用于驱动程序的 **IWiaItem** 后，请将命令发送到驱动程序以重新生成其树 (例如，在调用 **IWiaItem：:D evicecommand** 方法) 中向其发送 [WIA CMD \_ SYNCHRONIZE](wia-driver-command-support.md)命令。 Microsoft Windows SDK 文档中介绍了 **CoCreateInstance**、 **IWiaDevMgr** 和 **IWiaItem** 。

刷新 WIA 项树的另一种方法是在 WIA 驱动程序中创建命名 [事件](wia-driver-event-support.md) 。 WIA 驱动程序中的线程随后可以等待此事件发出信号。 每次通过 TWAIN 驱动程序删除或添加图像时，TWAIN 驱动程序会通过调用此命名事件) # A3 的 Windows SDK 文档中所述的 (**SetEvent** 来 (。 然后，将释放 WIA 驱动程序中的线程，WIA 驱动程序将重建树。

无论采用哪种方式，都应该重建树，使其反映对照相机或扫描仪上的实际图像所做的任何更改。 确保每次更新树时，都要通过从项树中添加或删除项来对事件进行排队 (例如，将 "WIA \_ 事件 \_ 项 \_ 已删除" 或 "wia" \_ 事件 \_ 树 \_ 更新 (有关这些和其他 WIA 事件标识符的说明，请参阅 Windows SDK 文档) # A3。 如果在树发生更改时成功发送事件，这将解决我的电脑和其他 WIA 应用程序未自动更新的问题。

**注意**   尽管你的 TWAIN 和 WIA 驱动程序可能存在于同一个 DLL 中，但 WIA 和 TWAIN 驱动程序不能共享相同的 UI。 每个驱动程序都必须有自己的 UI。

 

 

 




