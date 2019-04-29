---
title: MUX 中间驱动程序安装
description: MUX 中间驱动程序安装
ms.assetid: 9d0c6d6f-c12f-4921-b08a-b23b7d96ccd9
keywords:
- MUX 中间驱动程序 WDK
- NDIS MUX 中间驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c05a055a4a2363e830364e2234c2af1f6b7ba6a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382627"
---
# <a name="mux-intermediate-driver-installation"></a>MUX 中间驱动程序安装





本主题概述 MUX 中间驱动程序安装问题。 有关中间驱动程序 INF 文件结构的其他信息，请参阅[网络 MUX 中间驱动程序的安装要求](installation-requirements-for-network-mux-intermediate-drivers.md)。

MUX 中间驱动程序需要两个 INF 文件。 协议 INF 文件定义协议下边缘的安装参数。 微型端口 INF 文件定义虚拟微型端口上边缘的安装参数。 设置**类**INF 文件进入**Net**虚拟微型端口 INF 文件中并**NetTrans**协议 INF 文件中。 下面的代码示例演示**类**协议 INF 文件项。

```INF
Class = NetTrans
```

*DDInstall* MUX 中间驱动程序 INF 文件中的部分必须具有**特征**条目。 定义**特征**协议 INF 文件如以下代码示例所示中的条目。

```INF
Characteristics = 0x80
```

NCF\_HAS\_UI (0x80) 需要启用自定义属性页中，在这种情况下是通知对象

定义**特征**微型端口 INF 文件如以下代码示例所示中的条目。

```INF
Characteristics = 0x21
```

**特征**0x21 值指示 NCF\_虚拟 (0x1) 和 NCF\_不\_用户\_可移动标志设置为 (0x20)。 NCF\_虚拟指定设备为虚拟适配器。 NCF\_不\_用户\_可移动是可选的指定用户不能删除中间驱动程序。 如果你想要隐藏从用户 （你不应这样做如果您的用户必须手动安装的设备） 的虚拟微型端口可以定义 NCF\_HIDDEN (0x8) 标志。 NCF\_*Xxx* Netcfgx.h 中定义的标志。 有关详细信息**特征**条目，NCF\_*Xxx*标记，请参阅[DDInstall 部分](ddinstall-section-in-a-network-inf-file.md)。

*DDInstall* MUX 中间驱动程序的协议 INF 文件部分必须包含**Addreg**指令**Ndi**密钥。 有关详细信息，请参阅[Adding Service-Related 值到 Ndi 密钥](adding-service-related-values-to-the-ndi-key.md)并[DDInstall.Services 部分](ddinstall-services-section-in-a-network-inf-file.md)。

中间 MUX 驱动程序时，除了 INF 文件中，您必须还提供通知对象。 通知对象负责安装虚拟微型端口。 引用具有的通知对象**ComponentDll**在协议 INF，如下所示的条目：

```INF
HKR, Ndi,            ComponentDll,   , mux.dll
```

用户安装它定义配置参数，将安装文件复制并还会安装通知对象 DLL 的协议 INF 文件。 用户将添加虚拟微型端口通过用户界面提供的通知对象。 微型端口 INF 文件应定义**ExcludeFromSelect**条目来防止用户安装的微型端口 INF 文件而不是协议 INF 文件。

该驱动程序注册的协议名称必须匹配的服务名称。

```INF
HKR, Ndi, Service, 0, MUXP
```

**UpperRange**并**LowerRange** INF 文件条目确定 MUX 中间驱动程序的绑定。 协议 INF 文件必须定义协议边缘绑定，如以下代码示例所示。

```INF
HKR, Ndi\Interfaces, UpperRange,    0,          "noupper"
HKR, Ndi\Interfaces, LowerRange,    0,          "ndis5"
```

微型端口 INF 文件必须定义的上边缘绑定，如以下代码示例所示。

```INF
HKR, Ndi\Interfaces,    UpperRange, 0,  "ndis5"
HKR, Ndi\Interfaces,    LowerRange, 0,  "nolower"
```

应将为"ndis5"在上述代码示例中使用的协议绑定所需的驱动程序。 有关中间驱动程序绑定的详细信息和**UpperRange**/**LowerRange**条目，请参阅[中间驱动程序 UpperRange 和 LowerRange INF 文件条目](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)。

 

 





