---
title: C28650
description: 为其使用 0 的类型不会将它视为失败的情况。
ms.assetid: faa24e4b-327c-42c7-92ee-33cd7b6ce5cb
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28650
ms.openlocfilehash: b8d17b0650bd63b7b7741b285c8e400290232077
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345889"
---
# <a name="c28650"></a>C28650


警告 C28650:要为其类型 ！ 0 是正在使用不会将它视为失败的情况。

如返回状态值 ！TRUE 是为返回表示失败的状态值不相同。

某些数据类型，如**NTSTATUS**并**HRESULT**具有关联的这些类型的值归入成功或失败的宏。 这些宏检查返回的值或值，以确定这一点的最高有效位。 因此，0 和 1 都归类为成功的值。

若要解决此警告的正确方法是返回正确的错误代码而不是一个泛型值，例如-1。

 

 





