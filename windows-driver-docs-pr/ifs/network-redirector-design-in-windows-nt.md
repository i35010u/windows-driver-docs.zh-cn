---
title: Windows NT 中的网络重定向程序设计
description: Windows NT 中的网络重定向程序设计
keywords:
- 网络重定向 WDK，Windows NT
- 重定向程序驱动程序 WDK、Windows NT
- 内核网络重定向 WDK、Windows NT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f772152e7b27770b2a8e2310f2ce2f41028bc9d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832701"
---
# <a name="network-redirector-design-in-windows-nt"></a>Windows NT 中的网络重定向程序设计


## <span id="ddk_network_redirector_design_in_windows_nt_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_IN_WINDOWS_NT_IF"></span>


为网络重定向程序实现内核模式驱动程序的体系结构在一段时间内已发生更改。 通常，网络重定向器的一般模型基于实现 Microsoft 网络的客户端内核驱动程序的体系结构 (LAN Manager 客户端) 。 Windows NT 3.0 中引入的原始方案使用的不是共享组件，并且受到限制。 此模型通常称为原始 rdr 驱动程序模型 (rdr 是重定向程序) 的缩写。 未提供操作系统的特殊支持来简化写入网络重定向程序的过程。 每个内核模式驱动程序都实现了网络重定向器所需的所有功能。 因此，每个内核驱动程序都将包含大量的代码，用于与 i/o 管理器、缓存管理器和内存管理器进行交互。 ) 例如，在 Windows 上安装的每个网络重定向器 (都必须实现所有这些功能。 此设计模型用于通过 Windows NT 4.0 的网络重定向器驱动程序。 下面是此体系结构的关系图，其中包含多个重定向器。

![说明 windows nt 中的网络重定向程序设计的示意图](images/redir-01.png)

 

 




