---
title: 从扫描仪存储传输数据
description: 从扫描仪存储传输数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c1ddbea2c740a262f3903288d9d8de5033f7c53
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819545"
---
# <a name="transferring-data-from-scanner-storage"></a>从扫描仪存储传输数据


若要从扫描程序存储项传输数据，WIA 应用程序应枚举根存储项所包含的存储文件夹和文件项，并使用每个单独的文件项作为传输源 (传输该特定项) 包含的数据。

对于 **WiaItemTypeImage** 文件项，应用程序可以读取现有的 wia \_ IPS \_ *Xxx* 或 WIA \_ IPA \_ *xxx* (或) 描述图像格式的属性 (如果支持) 。 应用程序还可以使用此信息从扫描程序存储中选择要下载的映像。

若要将数据传输到某个扫描仪存储文件夹项，WIA 应用程序应枚举可用的存储文件夹项，选择一个文件夹或创建一个新的文件夹项，然后将数据上传到其中。

**注意**  不应允许在根存储文件夹之外使用此枚举操作。

 

 

 




