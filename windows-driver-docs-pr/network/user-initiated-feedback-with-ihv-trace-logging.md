---
title: 用户启动的有关 IHV 跟踪日志记录的反馈概述
description: 本节中的主题概述了在用户启动的反馈 (UIF) 报表 (通过反馈工具提交) 期间收集详细 IHV 跟踪日志所需的步骤。
ms.assetid: BDD02AA2-A771-4AC1-B9D2-E9E8FA073B7A
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1910110cc2507a08ece4bbb8ed717b63341eaa98
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565693"
---
# <a name="user-initiated-feedback-with-ihv-trace-logging-overview"></a>用户启动的有关 IHV 跟踪日志记录的反馈概述

本节中的主题概述了在用户启动的反馈 (UIF) 报表 (通过反馈工具提交) 期间收集详细 IHV 跟踪日志所需的步骤。 在两种不同的情况下, 反馈工具会收集日志。 第一种方案是用户启动反馈时系统的快照。 在此期间, Windows 将收集 WMI 自动记录器和一些其他快照数据。 第二种情况涉及到用户重现该问题。 在此反馈过程中, Windows 将启动记录器, 其中包含更详细的日志记录和更大的文件大小, 以便为重现收集尽可能多的数据。 本部分介绍适用于每个反馈方案的 Ihv 的预期。

本节内容：

- [日志记录方案](logging-scenarios.md)
- [用户启动的反馈-正常模式](user-initiated-feedback-normal-mode.md)
- [用户启动的反馈-重现模式](user-initiated-feedback-repro-mode.md)
