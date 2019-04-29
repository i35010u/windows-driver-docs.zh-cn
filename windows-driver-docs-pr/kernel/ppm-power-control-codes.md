---
title: PPM 电源控制代码
description: 本主题中所述的电源控制代码使用平台扩展插件 (Pep)。
ms.assetid: 4BA89D0F-78F0-44DF-BC9B-0F9F3256CD59
keywords:
- PPM 电源控制代码
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 11fdc731ded56ed58243887071f7504a49e79a2b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369137"
---
# <a name="ppm-power-control-codes"></a>PPM 电源控制代码

本主题中所述的电源控制代码使用平台扩展插件 (Pep)。 电源控制请求将类似于 I/O 控制 (IOCTL) 请求。 与不同 IOCTL，但是，电源控制请求直接发送到窗口电源管理框架 (PoFx) 且未观察到的其他设备堆栈中的设备驱动程序。

PPM 电源控制代码如下：

|代码 |语法 |描述 |
|---|---|---|
|PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE|<p> // {38BD8901-AB20-4908-ABAA-AC34674BDFF3}</p><p>DEFINE_GUID(PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE, </p><p>0x38bd8901、 0xab20、 0x4908、 0xab，0xaa、 0xac，0x34、 0x67，0x4b 放、 0xdf，0xf3);</p>| PEP 使用代码来查询 Windows 电源管理框架 (PoFx) 分配给某个处理器的停置页有关的信息。 <p>若要确定适用于处理器的停置页的平台扩展插件 (PEP) 此处理器 PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE 电源控制将请求提交到 PoFx。</p> <p>若要启动此电源控制请求，PEP 首先调用 RequestWorker 例程，以通知 PoFx PEP 具有要提交的工作项。 通过将 PEP_DPM_WORK 通知发送到 PEP，PoFx 响应此调用。 PEP 通过提交停置页信息的电源控制工作请求做出响应。 此请求包括 PEP 分配 PEP_WORK_INFORMATION 结构，WorkType 成员设置为 PepWorkRequestPowerControl，，PowerControl 成员指向 PEP 分配 PEP_WORK_POWER_CONTROL 结构。 PEP_WORK_POWER_CONTROL 结构的 PowerControlCode 成员设置为 PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE。 此结构的 InBuffer 成员必须为 NULL，且 OutBuffer 成员必须指向 PEP 分配 PEP_PPM_CONTEXT_QUERY_PARKING_PAGE 结构。 此电源控制请求的响应，PoFx 停置页的虚拟和物理地址写入 PEP_PPM_CONTEXT_QUERY_PARKING_PAGE 结构。</p><p>PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE 电源控制请求是特定于 ARM 的和不支持在 x86 和 x64 处理器。 在 ARM 多处理器系统中，停置页是内存的 4 千字节块的操作系统使用为邮箱来控制正在启动从空闲状态的处理器。 PEP 可能使用的邮箱的某部分来存储特定于处理器的上下文数据。 有关详细信息，请参阅文档在标题为"ARM 平台的多处理器启动" https://www.acpica.org/related-documents。</p>|
|GUID_PPM_PERF_CONSTRAINT_CHANGE|<p> // {29181FA1-4BF3-4c2e-B314-A6D226322B00}</p><p>DEFINE_GUID(GUID_PPM_PERF_CONSTRAINT_CHANGE,</p><p>0x29181fa1、 0x4bf3、 0x4c2e、 0xb3，0x14、 0xa6<，0xd2、 0x26，0x32、 0x2b、 0x0);</p>|PEP 使用代码以通知 Windows 电源管理框架 (PoFx) 的处理器的性能限制，必须更改以适应外部约束 （电源预算工作、 热量约束、 电源，等）。 <p>没有输入或输出缓冲区用于此控制代码。</p><p>若要启动此电源控制请求，PEP 首先调用 RequestWorker 例程，以通知 PoFx PEP 具有要提交的工作项。 通过将 PEP_DPM_WORK 通知发送到 PEP，PoFx 响应此调用。 PEP 通过提交性能约束更改电源控制工作请求做出响应。 此请求包括 PEP 分配 PEP_WORK_INFORMATION 结构，WorkType 成员设置为 PepWorkRequestPowerControl，，PowerControl 成员指向 PEP 分配 PEP_WORK_POWER_CONTROL 结构。 PEP_WORK_POWER_CONTROL 结构的 PowerControlCode 成员设置为 GUID_PPM_PERF_CONSTRAINT_CHANGE。 此结构的 InBuffer 和 OutBuffer 成员必须为 NULL。 在对此电源控制请求的响应，PoFx 将将 PEP_NOTIFY_PPM_PERF_CONSTRAINTS 通知发送到 PEP 来获取新的处理器性能限制。</p>
 

 

