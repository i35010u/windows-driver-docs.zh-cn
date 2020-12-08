---
title: 取消数据传输
description: 取消数据传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01f701cf5496638f3a3550f644fcf1239e9e96dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785207"
---
# <a name="canceling-a-data-transfer"></a>取消数据传输





WIA 应用程序和 WIA 微型驱动程序可以随时取消数据传输。 WIA 微型驱动程序可以通过检查 [**IWiaMiniDrvCallBack：： MiniDrvCallback**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback) 方法返回的值来确定应用程序是否取消了数据传输。 如果该方法返回 S \_ FALSE，则数据传输已取消。 WIA 微型驱动程序必须停止所有获取活动并返回到空闲状态。 然后，它可以用于下一个数据传输。

WIA 微型驱动程序可以通过返回 \_ [**IWiaMiniDrv：:d rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 方法中的 FALSE 来指示数据传输已取消。 某些设备在硬件上有一个 "取消" 按钮，可以中止数据传输。 在这种情况下，WIA 微型驱动程序应返回 \_ FALSE。

**注意**   可以取消 WIA 扫描，而无需声明错误并返回 \_ FALSE。 但是，这种情况仅在 Windows XP 和更高版本的操作系统中可用;Windows Millennium Edition 中不可能出现这种情况。

 

从 **IWiaMiniDrvCallBack：： MiniDrvCallback** 方法收到的所有返回代码都应在 **IWiaMiniDrv：:d rvacquireitemdata** 方法中返回。 如果应用程序在 **IWiaMiniDrvCallBack：： MiniDrvCallback** 方法中返回错误代码，WIA 微型驱动程序必须停止数据传输，返回到空闲状态，然后将该错误代码返回到 WIA 服务。

 

