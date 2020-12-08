---
title: 使用 WSD 安装 WIA 扫描仪驱动程序
description: 使用 WSD 安装 WIA 扫描仪驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9b3497b19d637019120dc78e7ad8aca94d4231c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839253"
---
# <a name="installing-a-wia-scanner-driver-with-wsd"></a>使用 WSD 安装 WIA 扫描仪驱动程序


若要使用 WSD 安装 WIA 扫描器驱动程序，你应该使用 Windows Vista 中提供的 *WSDScan.sys* 内核模式驱动程序。 在 IRP \_ MN \_ 启动 \_ 设备期间， *WSDScan.sys* 读取 PKEY \_ PNPX \_ ID 设备属性，并将其保存到注册表中。 设备属性将写入设备密钥，该设备密钥在要安装的映像设备的注册表中创建，并将其写入 **CreateFileName** wia 注册表值 (这将在 [WIA 设备的 INF 文件](inf-files-for-wia-devices.md)) 中介绍。 当在 [**IStiUSD：： Initialize**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)方法期间进行 [**IStiDeviceControl：： GetMyDevicePortName**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)调用时，wia 服务会将此值返回到 wia 微型驱动程序。

使用 *WSDScan.sys* 的 web service 扫描器的 WIA 微型驱动程序在安装设备时已初始化其 **CreateFileName** 值。 若要初始化此值，WIA 微型驱动程序的 INF 文件必须引用 **STI。WSDSection** 和 **STI。WSDSection** 在微型驱动程序 inf 文件的 "**安装**" 和 "**服务**" 部分中的 *Sti* 文件中，如 [Web 服务扫描器的示例 inf 文件](sample-inf-file-for-a-web-services-scanner.md)中所示。

 

