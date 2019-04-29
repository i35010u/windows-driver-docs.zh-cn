---
title: 初始化
description: 初始化
ms.assetid: 7d5ee1c7-df6c-4394-9ba7-819ee7e9397b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 551c1446fa8bbc87651cfe99d1e896b14d735d40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359209"
---
# <a name="initialization"></a>初始化


LSI\_DriverEntry 例程中初始化 U3 Storport 微型端口驱动程序入口点。 其他重要的初始化例程是 LsiU3HWInitialize 和 LsiU3FindAdapter。 在后者中，驱动程序的同步模式设置为*StorSynchronizeFullDuplex*，这意味着该驱动程序可以接收新的请求，同时完成以前的请求。 换而言之，它可能会同时排队 Storport 来自新的请求时它正在以异步方式完成以前的请求。

 

 




