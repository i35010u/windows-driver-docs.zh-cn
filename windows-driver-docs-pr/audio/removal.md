---
title: HFP 设备删除
description: HFP 设备删除主题讨论 (了从音频系统)  (离开) 设备时，将会发生什么情况。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1097a33b6d3ac98d575533911825cc7a7c4abcec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800739"
---
# <a name="hfp-device-removal"></a>HFP 设备删除


HFP 设备删除主题讨论 (了从音频系统)  (离开) 设备时，将会发生什么情况。

若要为配对的 HFP 设备删除已注册的设备接口，音频驱动程序：

1. 取消任何挂起 \_ 的 IOCTL BTHHFP \_ 扬声器 \_ 获取 \_ 卷 \_ 状态 \_ 更新 IOCTLs。

2. 取消任何挂起 \_ 的 IOCTL BTHHFP \_ 流 \_ 获取 \_ 状态 \_ 更新 IOCTLs。

3. 取消任何挂起 \_ 的 IOCTL BTHHFP \_ 设备 \_ 获取 \_ 连接 \_ 状态 \_ 更新 IOCTLs。

4. 取消引用 HFP FileObject (这也取消了 DeviceObject) 的引用。

5. 调用 KsDeleteFilterFactory 以删除代表与删除的接口关联的 HFP 设备的筛选器工厂。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[操作理论](theory-of-operation.md)  



