---
title: SRV_OPEN 结构
description: SRV_OPEN 结构
ms.assetid: 6cf4c6f6-a21f-4919-92b5-2403b650d8d0
keywords:
- 服务器打开 WDK RDBSS
- 打开服务器 WDK RDBSS
- SRV_OPEN 结构
- 数据结构 WDK 文件系统
- RDBSS WDK 的文件系统、 连接和文件结构
- 重定向驱动器缓冲子系统 WDK 的文件系统、 连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- WDK RDBSS 的连接信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19af10d64c1f5d4200dcef515f113d26c83a4654
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541066"
---
# <a name="the-srvopen-structure"></a>SRV\_打开结构


## <span id="ddk_the_srv_open_structure_if"></span><span id="DDK_THE_SRV_OPEN_STRUCTURE_IF"></span>


SRV\_打开结构描述在服务器上所有打开文件。 多个文件的对象和文件对象扩展 (FOBXs) 可以共享同一 SRV\_打开结构如果匹配的访问权限。 例如，文件 ID 存储适用于中小型企业。 FCB 与相关联的文件 Id 列表。 同样，所有共享相同的服务器端打开的文件对象扩展此处列出了在一起。 此外，信息将存储有关是否打开一个新的 FCB 的可共享的服务器端打开上下文。

影响 SRV 的标志值\_打开操作将被拆分为两个组：

-   对网络微型-重定向程序可见的标志

-   在内部使用，通过 RDBSS 和对网络微型-重定向程序不可见的专用标志

对网络微型-重定向程序可见的标志包含可能 SRV 低 16 位\_打开标志。 较高的 16 位被保留供内部 RDBSS。

SRV\_打开结构包含以下：

-   签名和引用计数

-   FCB 结构反向指针

-   到 V 的反向指针\_NET\_根结构 （通常）

-   FOBX 结构的列表

-   访问权限和 collapsibility 状态

-   根据网络微型重定向或 SRV 的创建者的请求的其他存储\_打开结构

 

 




