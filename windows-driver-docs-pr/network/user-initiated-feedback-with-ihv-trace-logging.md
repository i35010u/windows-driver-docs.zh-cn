---
title: 用户使用 IHV 跟踪日志记录发起的反馈
description: 本部分中的本主题概述用于在用户启动反馈 (UIF) 报告通过反馈工具提交期间收集详细 IHV 跟踪日志所需的步骤。
ms.assetid: BDD02AA2-A771-4AC1-B9D2-E9E8FA073B7A
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 28e4767318dff87b7f98c3db24d783f72ac7960c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561520"
---
# <a name="user-initiated-feedback-with-ihv-trace-logging"></a>用户使用 IHV 跟踪日志记录发起的反馈

本部分中的本主题概述用于在用户启动反馈 (UIF) 报告通过反馈工具提交期间收集详细 IHV 跟踪日志所需的步骤。 有两个不同的方案的反馈工具将收集日志。 第一个方案是系统的在用户启动反馈时的时间的快照。 在此期间，Windows 收集 WMI 自动记录器和某些其他快照数据。 第二个方案涉及重现该问题的用户。 在这种反馈，Windows 使用更详细的日志记录和重现尽可能捕获尽可能多的数据的文件大小较大启动记录器。 本部分介绍 ihv 的每种反馈方案的期望。

本节内容：

- [日志记录方案](logging-scenarios.md)
- [用户启动的反馈-正常模式](user-initiated-feedback-normal-mode.md)
- [用户启动的反馈-重现模式](user-initiated-feedback-repro-mode.md)
