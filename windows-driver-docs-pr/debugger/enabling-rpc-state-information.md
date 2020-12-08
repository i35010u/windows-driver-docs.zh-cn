---
title: 启用 RPC 状态信息
description: 启用 RPC 状态信息
keywords:
- RPC 调试，启用 RPC 状态信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddaca1e126bd1e7b180bb572c222a9472a7e92d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820919"
---
# <a name="enabling-rpc-state-information"></a>启用 RPC 状态信息


## <span id="ddk_enabling_rpc_state_information_dbg"></span><span id="DDK_ENABLING_RPC_STATE_INFORMATION_DBG"></span>


可以收集两个不同级别的 RPC 运行时状态信息： **服务器** 信息和 **完整** 信息。 必须先启用此信息收集，然后才能使用调试器或 DbgRpc 来分析状态信息。

只有 Windows XP 和更高版本的 Windows 支持收集 RPC 状态信息。

收集 **服务器** 状态信息非常轻量。 每个 RPC 调用100计算机指令的开销，即使在性能测试期间没有可检测到的负载。 不过，收集此信息将使用内存 (大约每个 RPC 服务器 4KB) ，因此不建议在已遇到内存不足的计算机上执行此操作。 **服务器** 信息包括终结点、线程、连接对象和服务器调用 (SCALL) 对象的相关数据。 这足以调试大多数 RPC 问题。

收集 **完整** 状态信息更是重型。 它包括在 **服务器** 级别收集的所有信息，此外还包括客户端调用 (CCALL) 对象。 通常不需要 **完整** 的状态信息。

若要在单个计算机上收集状态信息，请 (Gpedit.msc) 运行组策略编辑器。 在 "本地计算机策略" 下，导航到 " **计算机配置/管理模板/系统/远程过程调用**"。 在此节点下，你将看到 " **维护 RPC 故障排除" 状态信息** 项。 在编辑其属性时，将看到五种可能的状态：

<span id="None"></span><span id="none"></span><span id="NONE"></span>**内容**  
不维护任何状态信息。 除非您的计算机遇到内存不足的情况，否则不推荐这样做。

<span id="Server"></span><span id="server"></span><span id="SERVER"></span>**服务**  
将收集 **服务器** 状态信息。 这是一台计算机上建议的设置。

<span id="Full"></span><span id="full"></span><span id="FULL"></span>**达到**  
将收集 **完整** 的状态信息。

<span id="Auto1"></span><span id="auto1"></span><span id="AUTO1"></span>**Auto1**  
在 RAM 小于 64 MB 的计算机上，这与 " **无**" 相同。 在 RAM 至少为 64 MB 的计算机上，这与 **服务器** 相同。

<span id="Auto2"></span><span id="auto2"></span><span id="AUTO2"></span>**Auto2**  
在运行 Windows Server 2003 （RAM 小于 128 MB）的计算机上或在任何 Windows XP 计算机上，这与 " **无**" 相同。 在至少具有 128 MB RAM 的 Windows Server 2003 计算机上，这与 **服务器** 相同。

这是默认值。

如果要同时在一组网络计算机上设置这些级别，请使用组策略编辑器将计算机策略部署到首选计算机集。 策略引擎将负责将所需的设置传播到首选计算机集。 在这种情况下， **Auto1** 和 **Auto2** 级别特别有用，因为操作系统和每台计算机上的 RAM 量可能会有所不同。

如果网络包括运行 windows XP 以前版本的 Windows 的计算机，则这些计算机上的设置将被忽略。

 

 





