---
title: 初始化
description: 初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 466f1ae760d572c1d13936ad996928dbfebc2857
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811711"
---
# <a name="initialization"></a>初始化


LSI \_ U3 Storport 微型端口驱动程序的入口点在 DriverEntry 例程中进行初始化。 其他重要的初始化例程是 LsiU3HWInitialize 和 LsiU3FindAdapter。 在后者中，驱动程序的同步模式设置为 *StorSynchronizeFullDuplex*，这意味着，当驱动程序完成以前的请求时，可能会收到新请求。 换句话说，它在异步完成以前的请求时，可能会同时将新请求从 Storport 排队。

 

 




