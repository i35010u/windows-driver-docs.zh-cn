---
title: V_NET_ROOT 结构
description: V_NET_ROOT 结构
ms.assetid: 866eba91-13b6-4b15-93de-4f627a635c92
keywords:
- 共享映射 WDK RDBSS
- V_NET_ROOT 结构 WDK RDBSS
- 映射共享
- 数据结构 WDK 文件系统
- RDBSS WDK 的文件系统、 连接和文件结构
- 重定向驱动器缓冲子系统 WDK 的文件系统、 连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- WDK RDBSS 的连接信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5b502f794a7214028576d9cb2b45a694839f63f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383850"
---
# <a name="the-vnetroot-structure"></a>V\_NET\_根结构


## <span id="ddk_the_v_net_root_structure_if"></span><span id="DDK_THE_V_NET_ROOT_STRUCTURE_IF"></span>


V\_NET\_根结构提供了映射到共享 （例如，用户驱动器映射的根目录下的相关联的共享点的点） 的机制。 V\_NET\_根名称可以是采用以下格式之一：

```cpp
\server\share\d1\d2
\;m:\server\share\d1\d2
```

名称的格式取决于是否存在本地设备 （"x:"，例如） 与此 V\_NET\_根结构。 在本地驱动器映射的情况下 (d1\\d2，例如)，本地驱动器映射到每台上获取前缀[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)打开上此 V\_NET\_根结构。

V\_NET\_根结构还用于提供备用凭据。 对于这种 V 目的\_NET\_根结构是将备用凭据传播到 NET\_根作为默认值。 为实现此目的，必须没有其他引用。

将出现的 v 形\_NET\_根结构由 RDBSS 维护于每个网络\_根。 每个 V\_NET\_根结构有几个元素中常见的其他 RDBSS 结构，和元素，是唯一的一个 V\_NET\_根结构。 管理 V RDBSS 例程\_NET\_根结构只能修改以下元素：

-   签名和引用计数

-   一个指向关联 NET\_根结构和链接

-   表查找 （前缀） 的名称信息

-   名称的前缀添加到任何名称用户会看到 (这是用于模拟 NET\_未映射的实际 NET 根目录下的根结构\_根结构)

V 进行收尾工作\_NET\_根结构由两部分组成：

1.  销毁所有 SRV 与关联的\_打开结构

2.  释放内存

可能会有这两个操作和 V 中的字段之间延迟\_NET\_根结构可防止第一步重复出现。

 

 




