---
title: MUX 中间驱动程序安装
description: MUX 中间驱动程序安装
keywords:
- MUX 中间驱动程序 WDK
- NDIS MUX 中间驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 566ed8908880d0dd707dafe35034640a48e0046b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815939"
---
# <a name="mux-intermediate-driver-installation"></a>MUX 中间驱动程序安装





本主题概述了 MUX 中间驱动程序安装问题。 有关中间驱动程序 INF 文件结构的其他信息，请参阅 [网络 MUX 中间驱动程序的安装要求](installation-requirements-for-network-mux-intermediate-drivers.md)。

MUX 中间驱动程序需要两个 INF 文件。 协议 INF 文件定义了协议下边缘的安装参数。 微型端口 INF 文件定义虚拟小型端口上边缘的安装参数。 将虚拟微型端口 INF 文件中的 " **类** INF 文件项" 设置为 " **网络** "，并将 **NetTrans** 在协议 INF 文件中。 下面的代码示例演示了协议 INF 文件的 **类** 条目。

```INF
Class = NetTrans
```

MUX 中间驱动程序 INF 文件中的 *DDInstall* 部分必须包含 **特征** 条目。 如下面的代码示例中所示，定义协议 INF 文件中的 " **特性** " 项。

```INF
Characteristics = 0x80
```

\_ \_ 若要启用自定义属性页（在本例中为 notify 对象），NCF 具有 UI (0x80) 

如下面的代码示例中所示，定义微型端口 INF 文件中的 **特征** 条目。

```INF
Characteristics = 0x21
```

" **特征** " 值0X21 指示 NCF \_ VIRTUAL (0X1) 和 NCF \_ \_ 标志设置为 "用户 \_ 可移动 () 0x20"。 NCF \_ virtual 指定设备是虚拟适配器。 NCF \_ \_ "不 \_ 删除用户" 是可选的，它指定用户不能删除中间驱动程序。 如果要从用户隐藏虚拟小型端口 (则不应执行此操作，如果用户必须手动安装设备) 可以定义 NCF \_ 隐藏 (0x8) 标志。 NCF \_ *Xxx* 标志在 Netcfgx 中定义。 有关 **特征** ENTRY 和 NCF \_ *Xxx* 标志的详细信息，请参阅 [DDInstall 部分](ddinstall-section-in-a-network-inf-file.md)。

MUX 中间驱动程序的协议 INF 文件的 *DDInstall* 部分必须包含 **Ndi** 键的 **Addreg** 指令。 有关详细信息，请参阅 [将 Service-Related 值添加到 Ndi Key](adding-service-related-values-to-the-ndi-key.md) 和 [DDInstall 部分](ddinstall-services-section-in-a-network-inf-file.md)。

除 INF 文件外，还必须提供包含 MUX 中间驱动程序的通知对象。 Notify 对象负责安装 virtual 微型端口。 按如下所示在协议 INF 中用 **ComponentDll** 项引用 notify 对象：

```INF
HKR, Ndi,            ComponentDll,   , mux.dll
```

用户安装协议 INF 文件，该文件定义配置参数、复制安装文件以及安装通知对象 DLL。 用户通过通知对象提供的用户界面添加 virtual 微型端口。 微型端口 INF 文件应定义 **ExcludeFromSelect** 条目，以防止用户安装微型端口 inf 文件而不是协议 inf 文件。

驱动程序注册的协议名称必须与服务名称匹配。

```INF
HKR, Ndi, Service, 0, MUXP
```

**UpperRange** 和 **LowerRange** INF 文件项确定 MUX 中间驱动程序的绑定。 协议 INF 文件必须定义协议边缘绑定，如下面的代码示例所示。

```INF
HKR, Ndi\Interfaces, UpperRange,    0,          "noupper"
HKR, Ndi\Interfaces, LowerRange,    0,          "ndis5"
```

微型端口 INF 文件必须定义上边缘绑定，如下面的代码示例所示。

```INF
HKR, Ndi\Interfaces,    UpperRange, 0,  "ndis5"
HKR, Ndi\Interfaces,    LowerRange, 0,  "nolower"
```

应该使用驱动程序所需的协议绑定替换前面的代码示例中的 "ndis5"。 有关中间驱动程序绑定和 **UpperRange** / **LowerRange** 条目的详细信息，请参阅 [中间驱动程序 UpperRange 和 LowerRange INF 文件条目](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)。

 

 





