---
title: PFA 结果的持久性
description: PFA 结果的持久性
ms.assetid: de79b87e-2c9a-4181-b531-8ad283bb9d5b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7290a26106ccdaee47377040ff17592d345b3e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340747"
---
# <a name="persistence-of-pfa-results"></a>PFA 结果的持久性


每当预测故障分析 (PFA) 预测内存页是可能失败，错误更正代码 (ECC) 根据当前 PFA 注册表设置，PFA 存储 (或*仍然存在*) 内存页的页帧数 (PFN). PFA 仍然存在中的列表中 PFN **{badmemory}** 引导配置数据 (BCD) 系统存储的对象。 此列表包含所有 PFA 具有预测可能会失败的内存页面 PFNs。 每当启动 Windows 操作系统时，它从正由系统中排除此列表中的内存页。

**请注意**  没有没有行业标准的映射到特定的物理内存模块的物理内存 PFN。 因此，WHEA 不能提供有关哪些内存模块发生故障的信息。

 

Windows 不提供自动的机制用于清除 BCD 系统存储中的此列表。 当发生故障的系统内存被替换，系统管理员必须通过使用 BCDEdit 命令行工具手动清除此列表。 如果不清除列表，则 Windows 仍将排除列表中的内存页不能被系统，即使有故障的内存已替换为模块。 有关使用 BCDEdit 工具管理 PFA 内存列表的详细信息，请参阅[How to Manage PFA 内存列表](how-to-manage-the-pfa-memory-list.md)。

 

 




