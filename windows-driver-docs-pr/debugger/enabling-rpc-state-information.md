---
title: 启用 RPC 状态信息
description: 启用 RPC 状态信息
ms.assetid: 8804d941-c241-44cb-8d91-05b94a875d94
keywords:
- RPC 调试、 启用 RPC 的状态信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6c3a5a9b29664527dec139283d56ef2ba31020d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564373"
---
# <a name="enabling-rpc-state-information"></a>启用 RPC 状态信息


## <span id="ddk_enabling_rpc_state_information_dbg"></span><span id="DDK_ENABLING_RPC_STATE_INFORMATION_DBG"></span>


可以收集两个不同级别的 RPC 运行时状态信息：**服务器**信息并**完整**信息。 调试程序前，必须启用收集此信息或 DbgRpc 可用于分析的状态信息。

只有 Windows XP 和更高版本的 Windows 支持 RPC 状态信息的收集。

收集**Server**状态信息是非常轻量。 它的费用为每个 RPC 调用，从而导致没有可检测的负载，即使在性能测试期间的大约 100 个机器指令。 但是，收集此信息使用内存 (大约 4 KB 每个 RPC 服务器)，因此不建议在已遇到内存不足的计算机上。 **服务器**信息包括有关终结点、 线程、 连接对象和服务器调用 (SCALL) 对象的数据。 这就足以调试大多数 RPC 问题。

收集**完整**状态信息非常详细的庞大。 它包括在收集的所有信息**Server**级别，此外，都包括客户端调用 (CCALL) 对象。 **完整**通常不需要状态信息。

若要启用要在单个计算机上收集状态信息，请运行组策略编辑器 (Gpedit.msc)。 根据本地计算机策略中，导航到**计算机配置/管理模板/系统/远程过程调用**。 此节点下你将看到**RPC 故障排除状态信息**项。 当您编辑其属性时，你将看到五个可能状态：

<span id="None"></span><span id="none"></span><span id="NONE"></span>**无**  
将不维护任何状态信息。 除非你的计算机遇到内存不足的情况，这不被建议。

<span id="Server"></span><span id="server"></span><span id="SERVER"></span>**Server**  
**服务器**将收集状态信息。 这是一台计算机上的推荐的设置。

<span id="Full"></span><span id="full"></span><span id="FULL"></span>**Full**  
**完整**将收集状态信息。

<span id="Auto1"></span><span id="auto1"></span><span id="AUTO1"></span>**Auto1**  
在具有少于 64 MB 的 RAM 的计算机，这是与相同**None**。 在使用至少 64 MB 的 RAM 的计算机，这是与相同**Server**。

<span id="Auto2"></span><span id="auto2"></span><span id="AUTO2"></span>**Auto2**  
使用小于 128 MB 的 RAM，运行 Windows Server 2003 的计算机上或在任何 Windows XP 计算机上，这是与相同**None**。 Windows Server 2003 计算机上至少 128 mb RAM，这是与相同**Server**。

这是默认设置。

如果你想要同时在一组联网的计算机上设置这些级别，使用组策略编辑器向计算机的首选集合推出计算机策略。 策略引擎将负责所需的设置将传播到计算机的首选集合。 **线自动 1**并**Auto2**级别是特别有用在这种情况下，因为操作系统和每台计算机上的 RAM 量可能会有所不同。

如果网络包含运行版本早于 Windows XP 的 Windows 的计算机，将在这些计算机上忽略的设置。

 

 





