---
title: 错误记录持久性机制
description: 错误记录持久性机制
ms.assetid: f361c966-7ed4-4676-afa9-75268196c0e4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3adaddcc33fb5bc4f2f43e3d2d5e21d0f8535826
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354441"
---
# <a name="error-record-persistence-mechanism"></a>错误记录持久性机制


错误记录持久性是一种机制依据[错误记录](error-records.md)可以存储在非易失性存储中。 因此，如果操作系统由于致命硬件错误条件而必须重新启动，将保留错误记录。 此机制，以便重新启动系统后会丢失任何致命硬件错误条件与相关的捕获的错误数据保留的错误记录。

系统重新启动以下致命硬件错误后，操作系统将查找并检索所有已存储在系统重新启动之前的错误记录。 在其中一个系统也无法返回到操作系统重新启动的情况下，系统固件或有权访问失败的系统的远程管理软件可以为了执行错误分析检索存储的错误记录。

特定于平台的硬件错误驱动程序 (PSHED) 实现之间的操作系统和硬件平台来保存和检索错误记录的错误记录持久性接口。 对于基于 x64 和基于 x86 的系统，PSHED 支持 ACPI 的错误记录的序列化表 (ERST)。 对于基于 Itanium 的系统，PSHED 支持硬件错误记录扩展到可扩展固件接口 (EFI) 运行时变量服务。 我们建议平台供应商在其硬件或固件中实现这些错误记录持久性机制。

如果硬件平台不实现硬件或固件受 PSHED 的错误记录持久性机制与兼容，平台供应商必须实现参与错误记录持久性 PSHED 插件。 与错误记录持久性机制的硬件平台实现此 PSHED 插件接口。 有关如何实现 PSHED 插件的详细信息，请参阅[特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)。

错误记录持久性支持 Windows Server 2008、 Windows Vista SP1 和更高版本的 Windows 中。

 

 




