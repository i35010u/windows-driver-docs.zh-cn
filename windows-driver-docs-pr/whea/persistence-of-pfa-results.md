---
title: PFA 结果的持久性
description: PFA 结果的持久性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebfdd4a5105e1f1c7de5540a44ee319153267ffc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787067"
---
# <a name="persistence-of-pfa-results"></a>PFA 结果的持久性


每当 (PFA 的预测故障分析) 预测到更正代码 (ECC) 内存页可能会基于当前 PFA 注册表设置失败时，PFA 存储 (或 *保持*)  () PFN 的页帧号。 PFA 会将 PFN 保存在引导配置数据的 **{badmemory}** 对象 (BCD) 系统存储区中。 此列表包含 PFA 预测的所有内存页的 PFNs 可能会失败。 当 Windows 操作系统启动时，它会排除系统使用的此列表中的内存页。

**注意**  将物理内存 PFN 映射到特定物理内存模块没有行业标准。 因此，WHEA 无法提供有关哪些内存模块发生故障的信息。

 

Windows 不会提供用于从 BCD 系统存储中清除此列表的自动机制。 当替换故障系统内存时，系统管理员必须使用 BCDEdit 命令行工具手动清除此列表。 如果未清除列表，则 Windows 将继续排除系统正在使用的列表中的内存页，即使已替换故障内存模块。 有关使用 BCDEdit 工具管理 PFA 内存列表的详细信息，请参阅 [如何管理 PFA 内存列表](how-to-manage-the-pfa-memory-list.md)。

 

 




