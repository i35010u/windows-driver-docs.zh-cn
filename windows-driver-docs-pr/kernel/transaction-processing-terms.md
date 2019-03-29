---
title: 事务处理的术语
description: 若要使用 KTM 在开始之前，您应该知道以下条款事务、 资源管理器、 事务客户端、 事务管理器、 日志流、 登记和事务处理系统的定义。
Robots: noindex, nofollow
ms.assetid: c8a8806f-a228-4d02-9995-c8cf45e57935
keywords:
- 内核事务管理器 WDK 术语
- KTM WDK 术语
- 事务 WDK KTM，定义
- 资源管理器 WDK KTM，定义
- 事务客户端 WDK KTM，定义
- 事务管理器 WDK KTM，定义
- 日志流 WDK KTM，定义
- 登记 WDK KTM，定义
- 事务处理系统 WDK KTM，定义
- TP WDK KTM 定义
- 事务 WDK KTM，术语
- 事务管理器 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bae9d3d11a3986f6eeb101f6cfddf278950c7f9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562880"
---
# <a name="transaction-processing-terms"></a>事务处理的术语


若要使用 KTM 在开始之前，应了解以下术语的定义：[事务](#ktm-term-transaction)，[资源管理器](#ktm-term-resource-manager)，[事务客户端](#ktm-term-transactional-client)， [事务管理器](#ktm-term-transaction-manager)，[日志流](#ktm-term-log-stream)，[登记](#ktm-term-enlistment)，并且[事务处理系统](#ktm-term-transaction-processing-system)。

<a href="" id="ktm-term-transaction"></a>**事务**  
一个*事务*是数据操作的集合。 所有操作必须都成功，事务才能都成功。 如果所有操作都成功，可以是事务*提交*（即，其结果可为永久性和公共）。 如果任何操作失败，事务必须*回滚*，（即，所有更改必须都删除，以便该数据位于同一个事务的操作开始前的状态）。

事务的操作都*原子*，*一致*，*独立*，以及*持久*(ACID)。

-   它们是原子的因为它们必须提交或回滚作为一个整体。

-   它们是一致的因为操作始终生成准确的结果，无论它们是提交还是回滚。

-   它们被隔离，因为之前已提交或回滚事务的操作，每个事务的结果不是对其他事务可见。

-   它们是持久的因为操作的结果已提交或回滚事务的操作后，会永久。

事务的示例是使用自动取款机 (ATM) 将资金从您的支票帐户转移到您的存款帐户时必须执行的操作组。 从您的支票帐户和信用额度到您的存款帐户的借方必须显示为一个原子操作。

操作，则事务的一部分是也称为*事务处理操作*。

<a href="" id="ktm-term-resource-manager"></a>**资源管理器**  
一个*资源管理器*是管理数据资源可以更新的事务处理操作的软件组件。 例如，如果您正在设计的数据库系统，你可能会提供的存储和检索数据库的数据的资源管理器。 一个简单[事务处理系统](#ktm-term-transaction-processing-system)(TPS) 可能具有只有一个资源管理器。

资源管理器通常还提供事务客户端可以调用来访问资源管理器的数据的公共接口。 例如，数据库的资源管理器可能会提供一组客户端可以调用来读取和写入到数据库的函数。

更复杂的 TP 可以有多个资源管理器，其中每个参与系统的事务时管理单独的数据库或其他资源。

有关资源管理器的详细信息，请参阅[资源管理器创建](creating-a-resource-manager.md)。

在某些情况下，一个资源管理器是*卓越*到其他资源管理器，可以启动提交操作。 此类资源管理器在 KTM，称为[上级事务管理器](creating-a-superior-transaction-manager.md)。

<a href="" id="ktm-term-transactional-client"></a>**事务客户端**  
一个*事务客户端*是访问支持的数据库资源管理器，通常通过调用资源管理器将导出的函数的软件组件。 客户端负责创建事务，执行的一组资源管理器支持，操作，然后通知事务管理器 (KTM) 事务应是可以提交或回滚。

有关事务的客户端的详细信息，请参阅[创建事务的客户端](creating-a-transactional-client.md)。

<a href="" id="ktm-term-transaction-manager"></a>**事务管理器**  
一个*事务管理器*，如 KTM，提供了基础结构，使事务客户端和资源管理器可相互通信。 它还跟踪每个事务 （但不是客户端和资源管理器处理的数据） 的状态。

事务管理器还可以在系统崩溃后协调恢复操作。

事务管理器并不知道的数据或构成事务的操作。 由客户端和资源管理器控制的数据和操作。

KTM 提供事务客户端可以调用的函数。 这些函数允许客户端创建、 提交和回滚的事务。

KTM 还提供了函数管理器可以调用该资源。 这些函数可使资源管理员，以便他们可以接收有关事务通知在事务中登记。 在事务中登记的资源管理器后，它可接收通知，当事务的客户端已准备好提交或回滚事务，或恢复操作发生。

<a href="" id="ktm-term-log-stream"></a>**日志流**  
一个*日志流*是记录到事务发生的事件的历史记录。 KTM 通过维护日志流[公用日志文件系统](using-common-log-file-system.md)(CLFS)。 KTM 记录每个事务的状态更改，以便在必要时，它可以支持回滚和恢复操作。

资源管理器还必须使用日志流记录数据和操作。

回滚操作需要 KTM 和资源管理器将事务和所有数据还原到初始状态。 KTM 和资源管理器中日志流记录的每个事务的初始状态，以便它们可以在回滚操作期间提取它。

在系统崩溃后执行恢复操作。 操作系统随后重新启动时，KTM 和资源管理器可以使用日志流内容重新生成事务的状态设置为在发生崩溃前的状态。

有关 KTM 中日志流的详细信息，请参阅[使用日志流与 KTM 一起](using-log-streams-with-ktm.md)。

<a href="" id="ktm-term-enlistment"></a>**enlistment**  
*登记*是资源管理器和事务之间的关联。 KTM 提供了一组资源管理器调用来创建和管理登记的函数。 资源管理器创建登记后，KTM 将在通知事务的状态发生更改时发送到资源管理器。

<a href="" id="ktm-term-transaction-processing-system"></a>**事务处理系统**  
一个*事务处理系统*(TPS) 是一系列事务管理器、 一个或多个资源管理器、 一个或多个日志流和一个或多个事务的客户端访问资源管理器的资源。

 

 




