---
title: C28650
description: 为其使用0的类型不会将其视为故障事例。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28650
ms.openlocfilehash: f2ee3c4494a3d3d90ed288b1246b7d99521d8665
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839783"
---
# <a name="c28650"></a>C28650


警告 C28650：使用！0的类型不会将其视为故障情况。

返回状态值，如！TRUE 与返回指示失败的状态值的值不同。

某些数据类型（如 **NTSTATUS** 和 **HRESULT** ）有关联的宏，这些宏将这些类型的值分类为成功或失败。 这些宏检查返回值的最高有效位以确定此值。 因此，0和1均分类为成功值。

解决此警告的正确方法是返回正确的错误代码而不是一般值，例如-1。

 

 





