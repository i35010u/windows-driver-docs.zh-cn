---
title: 事务处理的术语
description: 在开始使用 KTM 之前，应了解以下术语：事务、资源管理器、事务客户端、事务管理器、日志流、登记和事务处理系统的定义。
Robots: noindex, nofollow
ms.assetid: c8a8806f-a228-4d02-9995-c8cf45e57935
keywords:
- 内核事务管理器 WDK，术语
- KTM WDK，术语
- 事务 WDK KTM，定义
- 资源管理器 WDK KTM，定义
- 事务性客户端 WDK KTM，定义
- 事务管理器 WDK KTM，定义
- 日志流 WDK KTM，定义
- 登记 WDK KTM，定义
- 事务处理系统 WDK KTM，定义
- TPS WDK KTM，定义
- 事务 WDK KTM，术语
- 事务管理器 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fe305eb86937e1d4330035003f6d127cd533ec0
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402852"
---
# <a name="transaction-processing-terms"></a>事务处理的术语


在开始使用 KTM 之前，应了解以下术语的定义： [事务](#ktm-term-transaction)、 [资源管理器](#ktm-term-resource-manager)、 [事务客户端](#ktm-term-transactional-client)、 [事务管理器](#ktm-term-transaction-manager)、 [日志流](#ktm-term-log-stream)、 [登记](#ktm-term-enlistment)和 [事务处理系统](#ktm-term-transaction-processing-system)。

<a href="" id="ktm-term-transaction"></a>**事务所**  
*事务*是数据操作的集合。 所有操作必须成功，事务才会成功。 如果所有操作都成功，则可以 *提交* 事务 (也就是说，其结果可以是永久性的，并且是公共的) 。 如果任何操作失败，则必须 *回滚*事务， (即，必须删除所有更改，使数据在事务的操作开始) 之前处于同一状态。

事务的操作为 *原子*、 *一致*、 *隔离*和 *持久* (ACID) 。

-   它们是原子的，因为它们必须作为一个整体进行提交或回滚。

-   它们是一致的，因为操作始终产生准确的结果，无论是提交还是回滚操作。

-   它们是隔离的，因为在提交或回滚事务的操作之前，每个事务的结果对其他事务都不可见。

-   它们是持久的，因为在提交或回滚事务的操作后，操作的结果将是永久性的。

事务的一个示例是在使用自动取款机 (ATM) 将金钱从支票帐户转移到储蓄帐户时必须执行的一组操作。 支票帐户和信用额度的借记必须是单个原子操作。

作为事务的一部分的操作也称为 "事务 *处理" 操作*。

<a href="" id="ktm-term-resource-manager"></a>**资源管理器**  
*资源管理器*是一种软件组件，用于管理可由事务处理操作更新的数据资源。 例如，如果您正在设计数据库系统，则可以提供一个资源管理器来存储和检索数据库的数据。 简单的 [事务处理系统](#ktm-term-transaction-processing-system) (TPS) 可能只有一个资源管理器。

资源管理器通常还提供一个公共接口，事务客户端可以调用它来访问资源管理器的数据。 例如，数据库的资源管理器可能会提供一组函数，客户端可调用它们来读取和写入数据库。

更复杂的 TPS 可以拥有多个资源管理器，每个管理器都可以在参与系统事务时管理单独的数据库或其他资源。

有关资源管理器的详细信息，请参阅 [创建资源管理器](creating-a-resource-manager.md)。

在某些情况下，一个资源管理器 *优于* 其他资源管理器，并且可以启动提交操作。 在 KTM 中，此类资源管理器称为 [上级事务管理](creating-a-superior-transaction-manager.md)器。

<a href="" id="ktm-term-transactional-client"></a>**事务客户端**  
*事务性客户端*是一种软件组件，它访问资源管理器支持的数据库，通常通过调用资源管理器导出的函数。 客户端负责创建事务，执行资源管理器支持的一组操作，然后将事务管理器 (KTM) 应提交或回滚事务。

有关事务客户端的详细信息，请参阅 [创建事务客户端](creating-a-transactional-client.md)。

<a href="" id="ktm-term-transaction-manager"></a>**事务管理器**  
*事务管理器*（如 KTM）提供了基础结构，使事务客户端和资源管理器能够彼此通信。 它还跟踪每个事务 (的状态，但不跟踪客户端和资源管理器处理) 的数据。

事务管理器还可以在系统崩溃后协调恢复操作。

事务管理器不知道构成事务的数据或操作。 数据和操作由客户端和资源管理器控制。

KTM 提供事务性客户端可调用的函数。 这些函数使客户端能够创建、提交和回滚事务。

KTM 还提供资源管理器可调用的函数。 这些函数使资源管理器可以在事务中登记，以便它们可以接收有关事务的通知。 资源管理器在事务中登记后，当事务客户端准备好提交或回滚事务时，或在发生恢复操作时，它可能会收到通知。

<a href="" id="ktm-term-log-stream"></a>**日志流**  
*日志流*是事务发生的事件历史记录。 KTM 使用 [公用日志文件系统](introduction-to-the-common-log-file-system.md) (CLFS) 维护日志流。 KTM 记录每个事务的状态更改，以便在必要时可以支持回滚和恢复操作。

资源管理器还必须使用日志流来记录数据和操作。

回滚操作要求 KTM 和资源管理器将事务和所有数据还原到初始状态。 KTM 和资源管理器记录日志流中每个事务的初始状态，以便它们可以在回滚操作期间提取该状态。

在系统崩溃后发生恢复操作。 当操作系统重新启动时，KTM 和资源管理器可以使用日志流内容将事务状态重建为发生崩溃之前的状态。

有关 KTM 中日志流的详细信息，请参阅 [使用 ktm 的日志流](using-log-streams-with-ktm.md)。

<a href="" id="ktm-term-enlistment"></a>**登记**  
*登记*是资源管理器与事务之间的关联。 KTM 提供一组函数，资源管理器调用这些函数来创建和管理登记。 资源管理器创建登记后，当事务的状态发生更改时，KTM 向资源管理器发送通知。

<a href="" id="ktm-term-transaction-processing-system"></a>**事务处理系统**  
*事务处理系统* (TPS) 是事务管理器、一个或多个资源管理器、一个或多个日志流以及一个或多个访问资源管理器资源的事务客户端的集合。

 

 




