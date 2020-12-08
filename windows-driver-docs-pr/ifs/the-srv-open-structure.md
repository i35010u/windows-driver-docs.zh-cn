---
title: SRV_OPEN 结构
description: SRV_OPEN 结构
keywords:
- 服务器打开 WDK RDBSS
- 打开服务器 WDK RDBSS
- SRV_OPEN 结构
- 数据结构 WDK 文件系统
- RDBSS WDK 文件系统、连接和文件结构
- 重定向的驱动器缓冲子系统 WDK 文件系统、连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- 连接信息 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e41dc1f018c33c2207b0a63322ef9309c1d98d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832683"
---
# <a name="the-srv_open-structure"></a>SRV \_ 开放式结构


## <span id="ddk_the_srv_open_structure_if"></span><span id="DDK_THE_SRV_OPEN_STRUCTURE_IF"></span>


SRV \_ 开放式结构描述服务器上的特定打开。 如果访问权限匹配，则多个文件对象和文件对象扩展 (FOBXs) 可以共享相同的 SRV \_ 开放结构。 例如，存储 Smb 的文件 ID。 文件 Id 的列表与 FCB 关联。 同样，在此处列出共享同一服务器端打开的所有文件对象扩展。 此外，还将存储有关新打开的 FCB 是否可以共享服务器端打开上下文的信息。

影响 SRV 打开操作的标志值 \_ 拆分为两个组：

-   网络小型重定向器的可见标志

-   RDBSS 在内部使用的专用标志，网络小型重定向程序不可见

网络小型重定向器的可见标志包含可能的 SRV 开放标志的较低16位 \_ 。 较高的16位保留供 RDBSS 在内部使用。

SRV \_ 开放式结构包含以下内容：

-   签名和引用计数

-   FCB 结构的反向指针

-   \_ \_ (通常) 的 .net 根结构的反向指针

-   FOBX 结构列表

-   访问权限和 collapsibility 状态

-   网络小型重定向程序或 SRV 开放式结构创建者请求的其他存储 \_

 

 




