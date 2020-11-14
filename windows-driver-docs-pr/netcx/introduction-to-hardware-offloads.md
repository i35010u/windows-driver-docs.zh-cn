---
title: NetAdapterCx 硬件卸载
description: NetAdapterCx 中的硬件卸载概述
ms.assetid: ''
keywords:
- WDF 网络适配器类扩展卸载，NetAdapterCx 硬件卸载，NetAdapterCx 卸载，Get-netadapter 卸载
ms.date: 10/09/2020
ms.custom: Fe
ms.openlocfilehash: d2e36d67821510251b244b3216eb7b64e51eafea
ms.sourcegitcommit: 5587af31b12cf96c1a31d42f7b40e8f72e3d739c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2020
ms.locfileid: "94572486"
---
# <a name="introduction-to-netadaptercx-hardware-offloads"></a>NetAdapterCx 硬件卸载简介

> [!WARNING]
> 本主题中的一些信息与预发布的产品相关，该产品在商业发布之前可能会进行重大修改。 Microsoft 对此处提供的信息不提供任何明示或暗示的保证。
>
> NetAdapterCx 仅在 Windows 10 版本2004中处于预览阶段。
>
> 目前，NetAdapterCx 客户端驱动程序无法通过认证。

为了提高性能，Windows TCP/IP 堆栈可以将一些任务卸载到网络接口卡， (NIC) 具有适当的任务卸载功能。

NetAdapterCx 重点介绍减轻卸载功能的配置和管理。 客户端驱动程序只需为其硬件卸载功能指定简单的配置，并注册回调即可通知功能发生的更改。 

本指南概述了 NetAdapterCx 中硬件卸载的主要概念。

- 硬件卸载功能是在初始化期间由网络适配器硬件公布的，并且必须在调用 [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)之前播发。
- 驱动程序无需检查标准注册表关键字。 NetAdapterCx 检查注册表关键字，并在启用活动卸载功能时遵循这些关键字。
- 网络适配器的 *活动* 卸载功能是当前用来对网络适配器进行编程以执行的功能。 这些是之前的客户端驱动程序公布的硬件功能的子集。
- TCP/IP 堆栈或过量协议驱动程序可以请求网络适配器的活动功能更改。 客户端驱动程序向 NetAdapterCx 注册回调，以便在活动卸载功能发生更改时收到通知。
- 如果某个卸载需要数据包扩展，则该扩展将在网络适配器为硬件卸载公布支持时自动注册。

客户端驱动程序为其硬件可卸载的网络数据包类型播发一组精细的功能 NetAdapterCx。 例如，这可以是 IPv4 选项、IPv6 扩展、TCP 选项或此类的任何组合是否受支持，等等。如果数据包标头偏移量已知，某些硬件只能执行卸载，并且此类硬件的客户端驱动程序还可以指定其数据包标头偏移量的限制。 例如，如果硬件描述符只有8位存储第4层标头偏移，则客户端驱动程序会将 Layer4HeaderOffset 设置为255。 客户端驱动程序功能未涵盖的任何数据包都将通过 NetAdapterCx 在软件中进行卸载。

如果硬件无法处理特定的组合，则在遇到此类数据包时，客户端驱动程序不应声明支持该功能，也不会执行软件回退。 相反，它应让 NetAdapterCx 自动执行任何必要的软件回退。

> [!NOTE]
> 如果你想要 NetAdapterCx 对硬件不支持的卸载执行软件回退，则客户端驱动程序必须在 INF 文件中包含该卸载的标准化关键字。 例如，如果客户端驱动程序不能在硬件上执行 RSC 卸载，并且需要 NetAdapterCx 在软件中执行此卸载，则 INF 中必须包含 * RscIpv4 和 * RscIpv6 关键字。

NetAdapterCx 和 Windows TCP/IP 堆栈支持以下卸载：

| 卸载名称 | 说明 |
| --- | --- |
| [检验](checksum-offload.md) | 将 IP 和 TCP 校验和的计算和验证卸载到 NIC。 |
| [通用发送卸载 (GSO) ](gso-offload.md) | 为 IPv4 和 IPv6 卸载大型 TCP/UDP 数据包的分段。 |
| [接受段合并 (RSC)](rsc-offload.md) | 为 IPv4 和 IPv6 卸载接收的 TCP 段序列的合并。 |

若要详细了解 TCP/IP 堆栈或过量协议驱动程序请求对网络适配器的活动功能的更改时配置卸载和更新卸载，请访问相应的 "卸载引用" 页。

