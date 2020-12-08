---
title: 错误记录持久性机制
description: 错误记录持久性机制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60de6747972a935b3ee8af1a647f83753f6df48c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837601"
---
# <a name="error-record-persistence-mechanism"></a>错误记录持久性机制


错误记录持久性是一种机制，通过该机制可以将 [错误记录](error-records.md) 存储在非易失性存储中。 因此，如果操作系统因致命硬件错误条件而必须重新启动，则会保留错误记录。 此机制将保留错误记录，以便重新启动系统时不会丢失任何与致命硬件错误条件相关的已捕获错误数据。

在出现严重硬件错误后重新启动系统后，操作系统将查找并检索在重新启动系统之前存储的所有错误记录。 在系统无法重新启动回操作系统的情况下，有权访问失败系统的系统固件或远程管理软件可以检索存储的错误记录，以便执行错误分析。

平台特定的硬件错误驱动程序 (PSHED) 在操作系统和硬件平台之间实现错误记录永久性接口以保存和检索错误记录。 对于基于 x64 和基于 x86 的系统，PSHED 支持 ACPI 错误记录序列化表 (ERST) 。 对于基于 Itanium 的系统，PSHED 支持 (EFI) 运行时变量服务的可扩展固件接口的硬件错误记录扩展。 建议平台供应商在其硬件或固件中实现这些错误记录持久性机制。

如果硬件平台未实现与错误记录 PSHED 支持的持久性机制兼容的硬件或固件，则平台供应商必须实现参与错误记录持久性的 PSHED 插件。 此 PSHED 插件接口具有由硬件平台实现的错误记录持久性机制。 有关如何实现 PSHED 插件的详细信息，请参阅 [特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)。

Windows Server 2008、Windows Vista SP1 和更高版本的 Windows 支持错误记录持久性。

 

 




