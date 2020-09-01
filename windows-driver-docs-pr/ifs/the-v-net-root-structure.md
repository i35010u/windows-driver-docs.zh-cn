---
title: V_NET_ROOT 结构
description: V_NET_ROOT 结构
ms.assetid: 866eba91-13b6-4b15-93de-4f627a635c92
keywords:
- 共享映射 WDK RDBSS
- V_NET_ROOT 结构 WDK RDBSS
- 映射共享
- 数据结构 WDK 文件系统
- RDBSS WDK 文件系统、连接和文件结构
- 重定向的驱动器缓冲子系统 WDK 文件系统、连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- 连接信息 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8fdd338ae73c2245c041b758742ba218d2b768c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065924"
---
# <a name="the-v_net_root-structure"></a>\_.Net \_ 根结构


## <span id="ddk_the_v_net_root_structure_if"></span><span id="DDK_THE_V_NET_ROOT_STRUCTURE_IF"></span>


\_.Net \_ 根结构提供了一种映射到共享 (的机制，例如，指向关联共享点根下的用户驱动器映射) 。 \_NET \_ ROOT name 可以采用以下格式之一：

```cpp
\server\share\d1\d2
\;m:\server\share\d1\d2
```

名称的格式取决于是否存在 ( "X：" 的本地设备，例如) 与此 \_ .Net \_ 根结构关联的。 如果本地驱动器映射 (d1 \\ d2，例如) ，则本地驱动器映射将作为此[**CreateFile**](/windows/desktop/api/fileapi/nf-fileapi-createfilea) \_ .net 根结构上打开的每个 CreateFile 的前缀 \_ 。

\_.Net \_ 根结构还用于提供备用凭据。 这种类型的 \_ .Net 根结构的用途 \_ 是将备用凭据作为默认凭据传播到 NET \_ root。 为此，必须没有其他引用。

.Net 根结构的列表 \_ \_ 由 RDBSS 为每个 NET \_ root 维护。 每个 \_ .Net \_ 根结构都有几个与其他 RDBSS 结构共有的元素，以及对 \_ .net 根结构唯一的元素 \_ 。 管理 \_ .Net 根结构的 RDBSS 例程 \_ 仅修改以下元素：

-   签名和引用计数

-   指向关联的网络 \_ 根结构和链接的指针

-   表查找 (前缀) 的名称信息

-   要添加到用户看到的任何名称的前缀的名称 (此值用于模拟 \_ 未映射到实际网络根结构的根的网络根结构 \_) 

\_.Net \_ 根结构的完成由两部分组成：

1.  销毁与所有 SRV \_ 开放式结构的关联

2.  释放内存

这两个操作之间可能存在延迟，而 .Net 根结构中的字段 \_ 会 \_ 阻止复制第一步。

 

