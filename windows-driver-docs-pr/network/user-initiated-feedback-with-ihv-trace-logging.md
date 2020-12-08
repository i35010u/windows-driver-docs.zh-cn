---
title: “将用户发起的反馈与 IHV 跟踪日志记录配合使用”概述
description: 本节中的主题概述了在用户启动的反馈中收集详细 IHV 跟踪日志所需的步骤， (UIF) 通过反馈工具提交的报表。
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: bd7605ec7fe1bfd9284dba8c49ffb76ebce95f90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805147"
---
# <a name="user-initiated-feedback-with-ihv-trace-logging-overview"></a>“将用户发起的反馈与 IHV 跟踪日志记录配合使用”概述

本节中的主题概述了在用户启动的反馈中收集详细 IHV 跟踪日志所需的步骤， (UIF) 通过反馈工具提交的报表。 在两种不同的情况下，反馈工具会收集日志。 第一种方案是用户启动反馈时系统的快照。 在此期间，Windows 将收集 WMI 自动记录器和一些其他快照数据。 第二种情况涉及到用户重现该问题。 在此反馈过程中，Windows 将启动记录器，其中包含更详细的日志记录和更大的文件大小，以便为重现收集尽可能多的数据。 本部分介绍适用于每个反馈方案的 Ihv 的预期。

本节内容：

- [日志记录方案](logging-scenarios.md)
- [用户发起的反馈 - 正常模式](user-initiated-feedback-normal-mode.md)
- [用户发起的反馈 - 再现模式](user-initiated-feedback-repro-mode.md)
