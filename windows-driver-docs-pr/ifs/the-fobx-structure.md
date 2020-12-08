---
title: FOBX 结构
description: FOBX 结构
keywords:
- 引用计数 WDK RDBSS
- FOBX 结构
- FILE_OBJECT 结构
- 计数引用 WDK RDBSS
- backpointers WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 文件系统、连接和文件结构
- 重定向的驱动器缓冲子系统 WDK 文件系统、连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- 连接信息 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 840ba2097216a865ae8e102ed8b6a4cee2b9bcac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817337"
---
# <a name="the-fobx-structure"></a>FOBX 结构


## <span id="ddk_the_fobx_structure_if"></span><span id="DDK_THE_FOBX_STRUCTURE_IF"></span>


文件对象扩展 (FOBX) 结构是 [**文件 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object) 结构的 RDBSS 扩展。 FOBX 结构由文件对象中的 **FileObjectExtension** 字段指向。 FOBX 结构包含以下内容：

-   签名和引用计数

-   关联的 FCB 结构的反向指针

-   关联的 SRV \_ 开放式结构的反向指针

-   有关此开放结构的上下文信息

-   网络小型重定向程序或 FOBX 结构创建者请求的其他存储

FOBX 结构包含所需的所有信息，每个文件对象通常不是由 i/o 系统存储的。 有关文件对象的信息由 i/o 系统在固定大小的文件系统对象中进行存储。 FOBX 结构通过网络小型重定向程序处理文件对象上所需的其他信息。

文件对象中的 **FsContext2** 字段引用了任何文件对象的 FOBX 结构。 尽管 FOBX 结构通常是 RDBSS 结构中的终点，但目前仍对 FOBX 结构进行引用计数。

FOBX 标志拆分为两个组：

-   网络小型重定向器的可见标志

-   RDBSS 在内部使用的标志，网络小型重定向程序不可见

网络小型重定向器的可见标志包含可能的 FOBX 标志的低16位。 较高的16位保留供 RDBSS 在内部使用。

 

