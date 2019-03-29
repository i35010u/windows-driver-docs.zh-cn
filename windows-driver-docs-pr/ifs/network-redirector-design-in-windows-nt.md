---
title: Windows NT 中的网络重定向程序设计
description: Windows NT 中的网络重定向程序设计
ms.assetid: 1feb43a3-ee65-4446-b38b-8b3f9188f43d
keywords:
- 网络重定向程序 WDK、 Windows NT
- 重定向程序驱动程序 WDK、 Windows NT
- 内核网络重定向程序 WDK、 Windows NT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec0c50183bb7820bab4d93114102aa6d203f9606
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565215"
---
# <a name="network-redirector-design-in-windows-nt"></a>Windows NT 中的网络重定向程序设计


## <span id="ddk_network_redirector_design_in_windows_nt_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_IN_WINDOWS_NT_IF"></span>


随时间而变化的网络重定向程序实现的内核模式驱动程序的体系结构。 通常将网络重定向程序的通用模型基于 Microsoft 网络 （LAN 管理器客户端） 的客户端实现内核驱动程序体系结构中。 在 Windows NT 3.0 中引入的原始方案使用没有共享的组件和限制。 此模型通常称为原始 rdr 驱动程序模型 （rdr 已重定向程序的缩写词）。 提供从操作系统没有特殊支持是为了简化编写网络重定向程序的过程。 每个内核模式驱动程序实现的所有函数所需的网络重定向程序。 因此，每个内核驱动程序将包括大量的代码与 I/O 管理器、 缓存管理器和内存管理器之间的交互。 每个网络重定向程序 （LAN 管理器、 NetWare 和 NFS，例如） 安装在 Windows 上必须实现所有这些函数本身。 这种设计模型使用的驱动程序通过 Windows NT 4.0 网络重定向程序。 下面是此体系结构，具有多个重定向程序的关系图。

![说明在 windows nt 中的网络重定向程序设计的关系图](images/redir-01.png)

 

 




