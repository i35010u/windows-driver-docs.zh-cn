---
title: Storport 事件日志扩展
description: Storport 事件日志扩展
ms.assetid: 03b0bdef-cefa-4ad8-b9bf-a5f6b5f64cc6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2c5f904720bbb722cdf057a3a75c9d735dd255b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527100"
---
# <a name="storport-event-log-extensions"></a>Storport 事件日志扩展


许多其他类型的驱动程序，如 Storport 微型端口驱动程序必须在系统事件日志，以保留附加的存储设备的条件的通知的管理员创建项。 通常会以与设备相关的故障响应创建这些事件日志条目。 Windows 内核本身提供灵活的接口，用于创建事件日志条目，尽管 Storport 微型端口模型不允许微型端口驱动程序直接访问该接口。 实际上，Storport 提供包装内核的系统事件日志工具，而微型端口驱动程序使用的包装器来创建事件日志条目。

在版本的 Windows 7 之前的 Storport，Storport 的系统事件日志接口为微型端口驱动程序访问提供了到内核的系统事件日志工具，它会严重影响的微型端口事件日志条目的有用性的功能的一小部分。 对于 Windows 7 新 Storport 事件日志接口微型端口驱动程序的完全访问权限向提供 Windows 内核事件工具的功能。 此访问权限使微型端口驱动程序来创建在排查存储问题中真正有用的事件日志条目。

[**StorPortLogSystemEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff567428)作为扩展函数 Storport 实现，并可供使用的现有扩展的函数接口的微型端口驱动程序。 使用扩展的函数接口可避免对新的函数; 的直接动态链接引用通过避免该直接引用，使用新的函数的微型端口驱动程序正确加载操作系统上不支持函数，函数返回存储帐户是否不含\_状态\_不\_不实现时受支持。 这样一来，供应商可以创建在多个 OS 版本运行单个的微型端口驱动程序充分利用新的事件日志记录函数支持的。

 

 




