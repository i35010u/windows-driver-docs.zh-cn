---
title: PPM 电源控制代码
description: 本主题中所述的电源控制代码由平台扩展插件 (PEPs) 使用。
keywords:
- PPM 电源控制代码
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: d6f7652939824354dce8b6aaab8104c5aded6cf9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783867"
---
# <a name="ppm-power-control-codes"></a>PPM 电源控制代码

本主题中所述的电源控制代码由平台扩展插件 (PEPs) 使用。 电源控制请求类似于 i/o 控制请求 (IOCTL) 。 不过，与 IOCTL 不同，电源控制请求会直接发送到窗口电源管理框架 (PoFx) ，而不会由设备堆栈中的其他设备驱动程序观察到。

下面是 PPM 电源控制代码：

|代码 |语法 |说明 |
|---|---|---|
|PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE|<p> {38BD8901-AB20-4908-ABAA-AC34674BDFF3}</p><p>DEFINE_GUID (PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE， </p><p>0x38bd8901、0xab20、0x4908、0xab、0xaa、0xac、0x34 赋、0x67、0x4b、0xdf、0xf3) ;</p>| PEP 使用代码来查询 Windows 电源管理框架 (PoFx) ，获取有关分配给处理器的停车页的信息。 <p>若要确定处理器的停车页，此处理器 (PEP) 平台扩展插件向 PoFx 提交 PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE 电源控制请求。</p> <p>若要启动此电源控制请求，PEP 首先会调用 RequestWorker 例程，通知 PoFx PEP 有要提交的工作项。 PoFx 通过将 PEP_DPM_WORK 通知发送到 PEP 来响应此调用。 PEP 通过提交对停车场信息的电源控制工作请求来做出响应。 此请求包括一个 PEP 分配 PEP_WORK_INFORMATION 结构，其中 WorkType 成员设置为 PepWorkRequestPowerControl，而 PowerControl 成员指向 PEP 分配的 PEP_WORK_POWER_CONTROL 结构。 PEP_WORK_POWER_CONTROL 结构的 PowerControlCode 成员设置为 PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE。 此结构的 InBuffer 成员必须为 NULL，并且 OutBuffer 成员必须指向 PEP 分配的 PEP_PPM_CONTEXT_QUERY_PARKING_PAGE 结构。 为了响应此 power control 请求，PoFx 将停车场的虚拟地址和物理地址写入 PEP_PPM_CONTEXT_QUERY_PARKING_PAGE 结构。</p><p>PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE 电源控制请求是特定于 ARM 的，不支持 x86 和 x64 处理器。 在 ARM 多处理器系统中，停车场是一种 4 kb 的内存块，操作系统使用它作为邮箱来控制从空闲状态启动的处理器。 PEP 可能使用邮箱的某些部分来存储特定于处理器的上下文数据。 有关详细信息，请参阅标题为 "ARM 平台的多处理器启动" 的文档 https://www.acpica.org/related-documents 。</p>|
|GUID_PPM_PERF_CONSTRAINT_CHANGE|<p> {29181FA1-4BF3-4c2e-B314-A6D226322B00}</p><p>DEFINE_GUID (GUID_PPM_PERF_CONSTRAINT_CHANGE，</p><p>0x29181fa1、0x4bf3、0x4c2e、0xb3、0x14、0xa6<、0xd2、0x26、0x32、0x2b、0x0) ;</p>|PEP 使用代码通知 Windows 电源管理框架 (PoFx) 处理器的性能限制必须更改，以满足外部约束 (电源预算、温度限制、电源等) 。 <p>没有与此控制代码一起使用的输入或输出缓冲区。</p><p>若要启动此电源控制请求，PEP 首先会调用 RequestWorker 例程，通知 PoFx PEP 有要提交的工作项。 PoFx 通过将 PEP_DPM_WORK 通知发送到 PEP 来响应此调用。 PEP 通过提交电源控制工作请求来进行性能限制更改来做出响应。 此请求包括一个 PEP 分配 PEP_WORK_INFORMATION 结构，其中 WorkType 成员设置为 PepWorkRequestPowerControl，而 PowerControl 成员指向 PEP 分配的 PEP_WORK_POWER_CONTROL 结构。 PEP_WORK_POWER_CONTROL 结构的 PowerControlCode 成员设置为 GUID_PPM_PERF_CONSTRAINT_CHANGE。 此结构的 InBuffer 和 OutBuffer 成员必须为 NULL。 为了响应此电源控制请求，PoFx 会将 PEP_NOTIFY_PPM_PERF_CONSTRAINTS 通知发送到 PEP 以获取新的处理器性能限制。</p>
 

 

