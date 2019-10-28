---
title: 取消数据传输
description: 取消数据传输
ms.assetid: a7900968-df57-41d9-abb1-4d2c97517362
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0ffdf121fb9e80b3e148aea92866a096ef2e95a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840882"
---
# <a name="canceling-a-data-transfer"></a>取消数据传输





WIA 应用程序和 WIA 微型驱动程序可以随时取消数据传输。 WIA 微型驱动程序可以通过检查[**IWiaMiniDrvCallBack：： MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)方法返回的值来确定应用程序是否取消了数据传输。 如果该方法返回\_FALSE，则已取消数据传输。 WIA 微型驱动程序必须停止所有获取活动并返回到空闲状态。 然后，它可以用于下一个数据传输。

WIA 微型驱动程序可以通过从[**IWiaMiniDrv：:D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法返回\_FALSE，来表示数据传输已取消。 某些设备在硬件上有一个 "取消" 按钮，可以中止数据传输。 在这种情况下，WIA 微型驱动程序应返回\_FALSE。

**请注意**   可以在不声明错误的情况下取消 WIA 扫描，返回 S\_FALSE。 但是，这种情况仅在 Windows XP 和更高版本的操作系统中可用;Windows Millennium Edition 中不可能出现这种情况。

 

从**IWiaMiniDrvCallBack：： MiniDrvCallback**方法收到的所有返回代码都应在**IWiaMiniDrv：:d rvacquireitemdata**方法中返回。 如果应用程序在**IWiaMiniDrvCallBack：： MiniDrvCallback**方法中返回错误代码，WIA 微型驱动程序必须停止数据传输，返回到空闲状态，然后将该错误代码返回到 WIA 服务。

 

 




