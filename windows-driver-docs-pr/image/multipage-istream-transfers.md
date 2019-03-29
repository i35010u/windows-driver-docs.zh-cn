---
title: 多页 IStream 传输
description: 多页 IStream 传输
ms.assetid: 0d17cfa8-f200-4d87-a2cb-cfd8dbc24e1e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d6da0a66408ede46f7e7adb6756df8b0d03abaf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567748"
---
# <a name="multipage-istream-transfers"></a>多页 IStream 传输


通常情况下，数据传输请求时的项，该项目中的将数据传输，使用项目的属性指定的设置。 例如，如果应用程序在扫描程序的"平台"项，数据传输将导致从平板、 使用存储在"平台"项上的 WIA 属性中的设置扫描。

但是，在 Windows Vista 中，另一个类型的传输是可用： 多项传输，也称为*文件夹获取*。 在此类型的传输，应用程序请求传输从文件夹项目通过使用指定的标志 (WIA\_传输\_ACQUIRE\_子级)，并从每个叶节点，该文件夹中的传输中的传输结果项的子树。

本部分包括：

[在多页传输过程中的驱动程序行为](driver-behavior-during-multipage-transfers.md)

 

 




