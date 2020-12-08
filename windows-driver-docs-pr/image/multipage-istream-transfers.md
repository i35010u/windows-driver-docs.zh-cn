---
title: 多页 IStream 传输
description: 多页 IStream 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cb31c7ec597e31ad13000bf9f90013d6a45bcbe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827131"
---
# <a name="multipage-istream-transfers"></a>多页 IStream 传输


通常，在对某一项请求数据传输时，将使用该项的属性指定的设置来传输该项中的数据。 例如，如果某个应用程序在扫描仪的 "平板" 项上，则数据传输将使用存储在 "平板" 项的 WIA 属性中的设置来扫描该平台。

但是，在 Windows Vista 中，可以使用另一种传输类型：多项传输，也称为 *文件夹获取*。 在这种类型的传输中，应用程序通过使用指定的标志 (WIA 传输获取子项) 来请求从文件夹项传输， \_ \_ \_ 而传输会导致从该文件夹项的子树中的每个叶节点传输。

本节包括：

[在多页传输过程中的驱动程序行为](driver-behavior-during-multipage-transfers.md)

 

 




